Gitosis on DotCloud
===================

Quick setup::

  git clone git://github.com/jpetazzo/gitosis-on-dotcloud
  git push gito6 gitosis-on-dotcloud
  dotcloud run gito6.www cat /home/dotcloud/data/id_rsa > key
  chmod 600 key
  ssh-add key
  GITCLOUD="$(dotcloud info gito6.www | grep ssh:// | awk '{print $2}')"

And now you can do e.g.::

  git clone $GITCLOUD/gitosis-admin
  cd gitosis-admin
  cat >>gitosis.conf <<EOF
  [group foo]
  writable = foo
  members = @all
  EOF
  git commit -a -m 'add project foo'
  git push
  cd /some/git/repository
  git remote add gitosis $GITCLOUD/foo
  git push gitosis master

