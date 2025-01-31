---
category: help
layout: help
mirrorid: ubuntu-ports
---

# Ubuntu Ports 软件仓库镜像使用帮助

<form class="form-inline">
<div class="form-group">
	<label>是否使用 HTTPS</label>
	<select id="http-select" class="form-control content-select" data-target="#content-0">
	  <option data-http_protocol="https://" selected>是</option>
	  <option data-http_protocol="http://">否</option>
	</select>
</div>
</form>


<form class="form-inline">
<div class="form-group">
	<label>是否使用 sudo</label>
	<select id="sudo-select" class="form-control content-select" data-target="#content-0">
	  <option data-sudo="sudo " data-sudoE="sudo -E " selected>是</option>
	  <option data-sudo="" data-sudoE="">否</option>
	</select>
</div>
</form>



Ubuntu 的软件源配置文件是 `/etc/apt/sources.list`。将系统自带的该文件做个备份，将该文件替换为下面内容，即可使用选择的软件源镜像。



<form class="form-inline">
<div class="form-group">
  <label>Ubuntu 版本：</label>
    <select id="select-0-0" class="form-control content-select" data-target="#content-0">
      <option data-release_name="jammy" selected>22.04 LTS</option>
      <option data-release_name="lunar">23.04</option>
      <option data-release_name="kinetic">22.10</option>
      <option data-release_name="focal">20.04 LTS</option>
      <option data-release_name="bionic">18.04 LTS</option>
      <option data-release_name="xenial">16.04 LTS</option>
      <option data-release_name="trusty">14.04 LTS</option>
    </select>
</div>
</form>

<form class="form-inline">
<div class="form-group">
  <label>使用官方安全更新软件源：</label>
    <select id="select-0-1" class="form-control content-select" data-target="#content-0">
      <option data-security_mirror="# " data-security_official="" selected>是</option>
      <option data-security_mirror="" data-security_official="# ">否</option>
    </select>
</div>
</form>

<form class="form-inline">
<div class="form-group">
  <label>启用 proposed：</label>
    <select id="select-0-2" class="form-control content-select" data-target="#content-0">
      <option data-enable_proposed="# " selected>否</option>
      <option data-enable_proposed="">是</option>
    </select>
</div>
</form>

<form class="form-inline">
<div class="form-group">
  <label>启用源码镜像：</label>
    <select id="select-0-3" class="form-control content-select" data-target="#content-0">
      <option data-enable_source="# " selected>否</option>
      <option data-enable_source="">是</option>
    </select>
</div>
</form>

{% raw %}
<script id="template-0" type="x-tmpl-markup">
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb {{http_protocol}}{{mirror}}/ {{release_name}} main restricted universe multiverse
{{enable_source}}deb-src {{http_protocol}}{{mirror}}/ {{release_name}} main restricted universe multiverse
deb {{http_protocol}}{{mirror}}/ {{release_name}}-updates main restricted universe multiverse
{{enable_source}}deb-src {{http_protocol}}{{mirror}}/ {{release_name}}-updates main restricted universe multiverse
deb {{http_protocol}}{{mirror}}/ {{release_name}}-backports main restricted universe multiverse
{{enable_source}}deb-src {{http_protocol}}{{mirror}}/ {{release_name}}-backports main restricted universe multiverse

{{security_mirror}}deb {{http_protocol}}{{mirror}}/ {{release_name}}-security main restricted universe multiverse
{{security_mirror}}{{enable_source}}deb-src {{http_protocol}}{{mirror}}/ {{release_name}}-security main restricted universe multiverse

{{security_official}}deb http://ports.ubuntu.com/ubuntu-ports/ {{release_name}}-security main restricted universe multiverse
{{security_official}}{{enable_source}}deb-src http://ports.ubuntu.com/ubuntu-ports/ {{release_name}}-security main restricted universe multiverse

# 预发布软件源，不建议启用
{{enable_proposed}}deb {{http_protocol}}{{mirror}}/ {{release_name}}-proposed main restricted universe multiverse
{{enable_proposed}}{{enable_source}}deb-src {{http_protocol}}{{mirror}}/ {{release_name}}-proposed main restricted universe multiverse
</script>
{% endraw %}

<p></p>

<pre>
<code id="content-0" class="language-properties" data-template="#template-0" data-select="#http-select,#sudo-select,#select-0-0,#select-0-1,#select-0-2,#select-0-3">
</code>
</pre>


因镜像站同步有延迟，可能会导致生产环境系统不能及时检查、安装上最新的安全更新，不建议替换 security 源。

