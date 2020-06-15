# Ansible

## Key/CSR Generation with Vaulting

~~~ bash
export F=FQDN
export TLS_BITS=4096
export C=Canada
export ST=Ontario
export L=Toronto
export O=Company
export OU=Dept
export EMAIL=email@company.com

# Generate new key and csr
openssl req \
    -out "host_files/${F}/${F}.csr" \
    -new \
    -newkey rsa:${TLS_BITS} \
    -nodes \
    -keyout "host_vars/${F}/vault_tls_private_key" \
    -subj "/C=${COUNTRY}/ST=${ST}/L=${L}/O=${O}/OU=${OU}/CN=${F}/emailAddress=${EMAIL}"

# indent the key file
sed -i 's/^/\ \ /g' "host_vars/${F}/vault_tls_private_key"

# add YAML header for Ansible variable
sed -i '1s/^/---\ntls_private_key: |\n/' "host_vars/${F}/vault_tls_private_key"

# vault the TLS private key
ansible-vault \
    encrypt \
    "host_vars/${F}/vault_tls_private_key"
 ~~~
