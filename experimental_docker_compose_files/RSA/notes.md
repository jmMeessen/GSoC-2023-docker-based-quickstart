# notes

These are notes related to this SSH Agent test. It seems that RSA keys don't
work as expected while ed keys work.

## generating the controler's RSA key pair
- `ssh-keygen -t rsa -b 4096 -C "demo@jenkins.io" -f ./rsa-key`
- In quiet mode: `ssh-keygen -q -t rsa -b 4096 -N '' -C "demo@jenkins.io" -f ./rsa-key <<<y >/dev/null 2>&1`
    - Command `ssh-keygen -l -f ./rsa-key` yields the following result `4096 SHA256:swlECrcdKcyYjNeDpdUGgOQHz5TAx8R8yZB4e4MGUVk demo@jenkins.io (RSA)`

- to execute into the agent: `docker compose run jenkins_agent /bin/bash`

## Demo script
- cleaning the environment `docker compose down` `docker compose rm` `docker volume rm docker_jenkins_home`
- `docker compose up --force-recreate`
- docker compose -f 01_docker-compose.yaml up
- copy init token 
- open localhost:8080
- paste admin token
- install default plugins
- continue with the wizard (admin user creation and URL)
- click on `build executor status` knob to enter the node administration, click on `new node`
- give it a name and click on permanent node, then create
- configuration:
    - the remote root directory is `/home/jenkins`
    - add a label (ex the agent's name)
    - launch method
        - launch agents via ssh
        - host : `agent`
        - credentials: add (jenkins provider)
            - kind : SSH Username with private key
            - ID: SSH-key
            - username: jenkins
            - private key: enter directly. Paste the key
            - no passphrase
            - add
        - select the newly created SSH key
        - host key validation: Non verifying strategy
        - save





