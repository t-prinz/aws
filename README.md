# aws
AWS examples

ansible-playbook -i <inventory> -e <"cred_file=credentials_file"> -e "aws_project_vars=project_variables_file" <-e "aws_inventory_file=inventory_file">

#
# These playbooks uses boto to access AWS credentials.  An alternative is to assign the credentials
# to variables and then define the AWS environment variables as shown below.
#
#  environment:
#    AWS_ACCESS_KEY_ID: "{{ aws_access_key_id }}"
#    AWS_SECRET_ACCESS_KEY: "{{ aws_secret_access_key }}"
# 

# Things learned along the way

# The os type is specified as part of the instance definition because there seems to be no guaranteed way to detect
# it from the ami image.  One thing you can rely on is the presence of the instance value "platform,"
# which guarantees it is a Windows system.  Reference something along the lines of
#
#    - name: Print platform if it is defined
#      debug:
#        msg: "Platform for instance {{ item['item'].instances[0].tags.Name }} is {{ item['item'].instances[0].platform }}"
#      with_items: "{{ eip_info.results }}"
#      when: item['item'].instances[0].state.name == "stopped" and item['item'].instances[0].platform is defined
#
