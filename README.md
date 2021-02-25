# sshoney
sshoney is a SSH honeypot using cowrie for the actual honeypot and Splunk for data visualization. Cowrie is deployed on host, Splunk is deployed in a docker container. Depending on design requirements, cowrie and splunk can be hosted on the same machine, or different. Configuration of the Ansible inventory determines that.

## Usage
`ansible-playbook -i hosts main.yml`

## Configuration files
 - `hosts`: The Ansible inventory files. Place the IP of each machine below its respective role. A single machine can be used if it is entered twice.
 - `vars.yml`: Configuration specific for the cowrie install.
   - `new_ssh_port`: Port for host SSH to listen on. (Honeypot will take over port 22)
   - `honeypot_hostname`: The hostname that will appear when a user connects to the honeypot.
   - `TZ`: Timezone for cowrie.
   - `splunk_url`: The direct download link for the Splunk Universal Forwarder. You can get this directly from the Splunk download page.
- `droppings/environment.env`: Environment variables for Splunk Enterprise.
  - `SPLUNK_PASSWORD`: The password to use for the new Splunk Enterprise instance. In a free license this isn't used to authenticate but still must be set.
  - `SPLUNK_LICENSE_URI`: If a valid Splunk Enterprise license is purchased, that can be entered here. Otherwise the Splunk Enterprise Free is already defined for you.