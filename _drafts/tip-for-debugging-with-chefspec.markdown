---
layout: post
title: "Tip for debugging with Chefspec"
categories: DevOps Software Testing
ONHOLD: SHELVED IDEA BECAUSE MATCHERS FOR REAL RESOURCES ACTUALLY DO THIS FOR YOU
blurb: "My coworker Matt Green and I were recently running into an issue with our Chefspec testing where we were looking for a specific chef resource to be called, but we made an error in our test code and had trouble debugging it."
---

[matthewgreen]: https://github.com/tobami/littlechef
[fr]: https://github.com/sethvargo/chefspec/blob/v3.4.0/lib/chefspec/runner.rb#L195
[chefspecdocs]: http://code.sethvargo.com/chefspec/

Using `find_resources` in Chefspec
----------
My coworker [Matt Green][matthewgreen] and I were recently running into an issue with our Chefspec testing where we were looking for a specific chef resource to be called, but we made an error in our test code and had trouble debugging it. With a little bit of digging we found an easy way to see what calls were made for a resource using the function [find_resources][fr]. While the function here is documented it is not in any of the official chef_spec [documentation][chefspecdocs] and so I would caution actually using it in tests. We found it useful to either print out the run or using `pry` to drop into an interactive debugger for explore further.

```
describe 'reach::proxy' do
  let(:chef_run) { ChefSpec::Runner.new.converge('reach::proxy') }

  it 'installs the apache logging conf' do
    puts chef_run.find_resources('template')
    expect(chef_run).to render_file("/etc/apache2/conf.d/logging.con")
  end
end

------------

Failures:

reach::proxy
  includes apache recipes (FAILED - 1)
template[/etc/sysconfig/httpd]
template[apache2.conf]
template[apache2-conf-security]
template[apache2-conf-charset]
template[/etc/apache2/ports.conf]
template[/etc/apache2/sites-available/default]
template[/etc/apache2/mods-available/status.conf]
template[/etc/apache2/mods-available/alias.conf]
template[/etc/apache2/mods-available/autoindex.conf]
template[/etc/apache2/mods-available/dir.conf]
template[/etc/apache2/mods-available/mime.conf]
template[/etc/apache2/mods-available/negotiation.conf]
template[/etc/apache2/mods-available/setenvif.conf]
template[/etc/apache2/ports.conf]
template[/etc/apache2/mods-available/ssl.conf]
template[/etc/apache2/mods-available/deflate.conf]
template[/etc/apache2/mods-available/proxy.conf]
template[/etc/apache2/conf.d/logging.conf]
template[/etc/apache2/sites-available/reach-intproxy.conf]
template[/etc/network/if-pre-up.d/iptables_load]
template[/etc/iptables.d/all_established]
template[/etc/iptables.d/all_icmp]
template[/etc/iptables.d/ports_reach]

```

