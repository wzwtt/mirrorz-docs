**注意：本镜像是 lineageOS 源代码的镜像，如果是希望下载 lineage 的 rom，请访问 [Lineage ROM 使用帮助](../lineage-rom/) 。**

### 过程摘录

下载 repo 工具：

<tmpl z-lang="bash">
mkdir ~/bin
PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
</tmpl>

或者使用[git-repo 镜像](../git-repo/)

建立工作目录：

<tmpl z-lang="bash">
mkdir WORKING_DIRECTORY
cd WORKING_DIRECTORY
</tmpl>

初始化仓库：

<tmpl z-lang="bash">
repo init -u {{endpoint}}/LineageOS/android.git -b lineage-21.0 --git-lfs
</tmpl>

（如果已经有从 GitHub 同步的 lineageOS 源代码，可以从这里直接开始）

打开`.repo/manifests/default.xml`，将

<tmpl z-lang="xml">
  <remote  name="github"
           fetch=".."
           review="review.lineageos.org" />
</tmpl>

改成

<tmpl z-lang="xml">
  <remote  name="github"
           fetch="https://github.com/" />

  <remote  name="lineage"
           fetch="{{endpoint}}/"
           review="review.lineageos.org" />
</tmpl>

替换 AOSP 请参考 [AOSP 帮助](../AOSP/) 中「LineageOS 中对于 AOSP 的替换」一节

将

<tmpl z-lang="xml">
  <default revision="..."
           remote="github"
</tmpl>

改成

<tmpl z-lang="xml">
  <default revision="..."
           remote="lineage"
</tmpl>

同步源码树（以后只需执行这条命令来同步）：

<tmpl z-lang="bash">
repo sync
</tmpl>

### 异常处理
	
1. 部分仓库例如 `Lineage_framework_base` 同步的时候会出现 bundle 错误，这时候可以使用命令 `repo sync --no-clone-bundle` 进行同步。
