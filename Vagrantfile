
Vagrant.configure("2") do |config|
	PROJECT="anvils"
	RDIP="192.168.50.2"
    #RUNDECK_YUM_REPO="https://bintray.com/rundeck/rundeck-rpm/rpm"
    RUNDECK_YUM_REPO="https://bintray.com/rundeck/ci-staging-rpm/rpm"


	config.vm.box = "centos-63-x64"
	config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/centos-63-x64.box"


	config.vm.define :rundeck do |rundeck|
		rundeck.vm.hostname = "rundeck.anvils.com"
		rundeck.vm.network :private_network, ip: "#{RDIP}"
		rundeck.vm.provision :shell, :path => "install-rundeck.sh", :args => "#{RDIP} #{RUNDECK_YUM_REPO}"
		rundeck.vm.provision :shell, :path => "install-httpd.sh"
        rundeck.vm.provision :shell, :path => "install-rundeck-admin.sh", :args => "https://bintray.com/rerun/rerun-rpm/rpm http://#{RDIP}:4440"

		rundeck.vm.provision :shell, :path => "add-project.sh", :args => "#{PROJECT}"
	end
end
