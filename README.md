# my-ansible-recipes

This repository is a sample ansible recipes for ubuntu setup.

## Reference

- These recipes are based on the following page.
    - [Ansible ベストプラクティス](https://docs.ansible.com/ansible/2.9_ja/user_guide/playbooks_best_practices.html#content-organization)
    - [Ansibleを使って複数のサーバーにDockerをインストールする](https://note.com/shift_tech/n/n880f71e8e03b)
        - docker recipe is written in the above page.


## Require

- This recipe requires ansible version 2.12 or higher.
- This recipe uses some community collection or roles published in Ansible Galaxy.
    - See collections/requirements.yml and roles/requirements.yml

## Usage

### Directory structure

```bash
my-ansible-recipes/
├── License
├── README.md
├── collections
│   └── requirements.yml
├── inventories
│   └── local
│       ├── group_vars
│       │   └── local.yml
│       └── hosts
├── roles
│   ├── requirements.yml
│   ├── apt
│   │   ├── defaults
│   │   │   └── main.yml
│   │   └── tasks
│   │       └── main.yml
│   ├── docker
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── handlers
│   │   │   └── main.yml
│   │   └── tasks
│   │       └── main.yml
│   ├── google-chrome
│   │   ├── defaults
│   │   │   └── main.yml
│   │   └── tasks
│   │       └── main.yml
│   ├── jfrog-cli
│   │   ├── defaults
│   │   │   └── main.yml
│   │   └── tasks
│   │       └── main.yml
│   ├── sample
│   │   ├── defaults
│   │   │   └── main.yml
│   │   └── tasks
│   │       └── main.yml
│   ├── snap
│   │   ├── defaults
│   │   │   └── main.yml
│   │   └── tasks
│   │       └── main.yml
│   └── vscode
│       ├── defaults
│       │   └── main.yml
│       └── tasks
│           └── main.yml
└── site.yml
```

- This recipe's target is only your own Ubuntu machine. Therefore, hosts only defines localhost.
- The install recipes contain in "roles". 
    - "sample" is a task sample. This recipe isn't called in the main playbook.
- "site.yml" is the main playbook file.

### Prepare

- Install ansible, version 2.12 or higher. In the case of Ubuntu, install with the following commands.

```bash
$ sudo apt update
$ sudo apt install --no-install-recommends software-properties-common git 
$ sudo apt-add-repository --yes --update ppa:ansible/ansible
$ sudo apt install --no-install-recommends ansible 
```

- Do "git clone this repository" and install required collections and roles with using following command.

```bash
$ git clone https://github.com/tomoten-umino/my-ansible-recipes.git
$ cd my-ansible-recipes
$ ansible-galaxy install -r roles/requirements.yml 
$ ansible-galaxy install -r collections/requirements.yml 
```

### Command

- Use the following command in the root directory.

```bash
$ ansible-playbook -i inventories/local/hosts --ask-become-pass site.yml
```

## License

- This sample repository is licensed under WTFPL license. See the LICENSE for more information.
- However, "docker" recipe is the copied code from [Ansibleを使って複数のサーバーにDockerをインストールする](https://note.com/shift_tech/n/n880f71e8e03b).
