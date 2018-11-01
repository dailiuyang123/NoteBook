#  GitHub 在 Idea 中 项目初始化（遇到的坑）

  ##  安装 Git  Git.exe 

  ##  然后 配置 SSH KEY 
  
  ## 将在本地.ssh下生成的 public key 公钥 粘贴到 GitHub 上 SSH 内
  
  ## 注意 如果 你的 .ssh 下没有 known_hosts 文件 你直接 用Idea clone  以git方式 项目 会报 not read responstry 异常。
  
   ### 1 第一次clone项目 应该  打开 git.bash 以 git clone git@xxx.com 形式克隆项目  
   ### 2. 然后汇报 一个 警告 。继续克隆 项目成功后 。
   ### 3. 查看 .ssh下 如果出现 了 Known_hosts 文件。 下次 就可以直接用 Idea clone 即可。   