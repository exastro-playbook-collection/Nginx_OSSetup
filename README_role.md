# Ansible Role: Nginx\_OSSetup

# Trademarks
-----------
* Linuxは、Linus Torvalds氏の米国およびその他の国における登録商標または商標です。
* RedHat、RHEL、CentOSは、Red Hat, Inc.の米国およびその他の国における登録商標または商標です。
* Windows、PowerShellは、Microsoft Corporation の米国およびその他の国における登録商標または商標です。
* Ansibleは、Red Hat, Inc.の米国およびその他の国における登録商標または商標です。
* pythonは、Python Software Foundationの登録商標または商標です。
* Nginxは、Nginx Software Inc. の米国登録商標です。
* Crossplaneは、Upbound, Inc.の登録商標または商標です。
* NECは、日本電気株式会社の登録商標または商標です。
* その他、本ロールのコード、ファイルに記載されている会社名および製品名は、各社の登録商標または商標です。

## Description

本Ansble Roleは"Nginx"のOS設定を行います。
対象バージョンは以下のバージョンです。

- RHEL 7

設定内容は以下のとおりです。  

- OS設定前の準備  
    - nginxがインストールされています
- OS設定実施  
    - NginxのOS設定  
    - 環境変数などの設定 

## Supports

- 管理マシン(Ansibleサーバ)
  - Linux系OS（RHEL 7 または 8）
  - Ansible バージョン2.8 または 2.9
  - Python バージョン2.7 または 3.6

- 管理対象マシン(インストール対象マシン)
  - RHEL 7

## Requirements
- 管理マシン(Ansibleサーバ)
  * 管理対象マシンとroot権限でSSH通信可能であること。

## Role Variables

Role の変数値について説明します。

### Mandatory Variables

### Optional variables

以下の変数は任意で指定します。

- NginxのOS設定の関連変数
  * ''VAR\_Nginx\_status'': nginxサーバを設定します (string, 例："START" あるいは "STOP" あるいは "RELOAD")  
  * ''VAR\_Nginx\_auto'': nginxサービスが自動的に起動することを設定します (bool, 例：true あるいは false)  

## Dependencies

特にありません。

## Usage

1. 本Roleを用いたPlaybookを作成します。  
2. 必須変数を指定します。  
3. 任意変数を必要に応じて指定します。  
4. Playbookを実行します。  

## Example Playbook

インストールとすべての設定をする場合は、提供した以下のRoleを"roles"ディレクトリに配置したうえで、
以下のようなPlaybookを作成してください。

- フォルダ構成
~~~
  - roles/
    ・ Nginx_Install/
    ・ Nginx_OSSetup/
    ・ Nginx_Setup/
  - hosts
  - Nginx.yml
  - conf.yml
~~~

- マスターPlaybook サンプル「Nginx.yml」
~~~
# Nginx.yml
- hosts: Nginx
  roles:
    - role: Nginx_OSSetup
      VAR_Nginx_status: start
      VAR_Nginx_auto: true
      tags:
        - Nginx_OSSetup
~~~

## Running Playbook
- extra-vars を利用する場合の実行例
~~~sh
ansible-playbook Nginx.yml -i hosts --extra-vars="@conf.yml"
~~~

- host_vars を利用する場合の実行例  
 host_vars で指定したグループ名が server1 の場合
~~~sh
ansible-playbook Nginx.yml  -i hosts -l server1
~~~

- 本Roleのみを実行する場合は、 --tags "Nginx_OSSetup" を付け加える
~~~sh
ansible-playbook Nginx.yml -i hosts --extra-vars="@conf.yml" --tags "Nginx_OSSetup"
~~~

# Copyright
Copyright (c) 2020 NEC Corporation

# Author Information
NEC Corporation

