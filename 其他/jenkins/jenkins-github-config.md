# Jenkins 配置 GitHub 项目

## Github 生成 `Personal access tokens`

> `Github: Settings -> Developer settings -> Persional access tokens`

`Generate new token` -> `Token description`(输入token描述，如：ob-test) -> `Select scopes`(选择权限， 如repo|admin:repo_hook等) -> `Generate token`

token生成后，拷贝出来备用。

## Jenkins 配置

1. 系统管理
   
   ![config](snapshot/jenkins_github_config.png)

2. 系统设置
   
   ![setting](snapshot/jenkins_github_setting.png)

3. github server

    ![github server](snapshot/jenkins_github_add_server.png)

    ![github server](snapshot/jenkins_github_github_server.png)

4. 添加 token 凭据
   
   ![token](snapshot/jenkins_github_add_server_token.png)

5. token 配置
   
    ![token page](snapshot/jenkins_github_server_token_page.png)

    ![token](snapshot/jenkins_github_server_token_scecret.png)


    `secret` 输入框填入 github `Persional access token`
    ![token](snapshot/jenkins_github_server_token_secret2.png)

6. 选择凭据

    ![token](snapshot/jenkins_github_server_token_use.png)


## 新建一个自由风格的项目

1. 创建项目任务

    ![task](snapshot/jenkins_github_create_task.png)

2. 配置 GitHub 项目地址

    ![general](snapshot/jenkins_github_task_general_config.png)

3. 源码管理配置

    ![general2](snapshot/jenkins_github_task_general_config2.png)

4. 配置构建脚本（shell）
   
    [jenkins build shell](jenkins-build-shell.md)

5. 保存后构建