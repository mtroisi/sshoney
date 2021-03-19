# sshoney
sshoney is a SSH honeypot using cowrie for the actual honeypot and Splunk for data visualization. Cowrie is deployed on host, Splunk is deployed in a docker container. Depending on design requirements, cowrie and splunk can be hosted on the same machine, or different. Configuration of the Ansible inventory determines that.

## Usage
`ansible-playbook -i hosts main.yml`

Note: `allow_world_readable_tmpfiles = True` must be set in the ansible.cfg file.

## Configuration files
 - `hosts`: The Ansible inventory files. Place the IP of each machine below its respective role. A single machine can be used if it is entered twice.
 - `vars.yml`: Configuration specific for the cowrie install.
   - `new_ssh_port`: Port for host SSH to listen on other than 2222. (Honeypot will take over port 22, and uses 2222 to listen normally)
   - `honeypot_hostname`: The hostname that will appear when a user connects to the honeypot.
   - `splunk_server`: Hostname or IP address that the Splunk server can be reached over tcp port 9997. If Cowrie and Splunk are on the same machine, set to 127.0.0.1
   - `TZ`: Timezone for cowrie.
   - `splunk_url`: The direct download link for the Splunk Universal Forwarder. You can get this directly from the Splunk download page.

## Visualization
A sample dashboard has been included in the splunk directory. The source XML must be imported manually.
