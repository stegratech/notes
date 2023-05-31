## disable x on startup
```
sudo systemctl set-default multi-user.target
```
## enable x on startup
```
sudo systemctl set-default graphical.target
```

https://access.redhat.com/documentation/en-us/red_hat_subscription_management/1/html/quick_registration_for_rhel/registering-cmd

sudo subscription-manager register --username admin-example --password secret --auto-attach
sudo subscription-manager register --auto-attach

https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/virtualization_deployment_and_administration_guide/cloning_virtual_machines

https://access.redhat.com/solutions/175423
https://access.redhat.com/solutions/3544591

https://access.redhat.com/discussions/2941211

https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/virtualization_deployment_and_administration_guide/cloning_virtual_machines


## registering a system without providing credentials
https://access.redhat.com/solutions/3341191

# generate a new activation key
https://access.redhat.com/management/activation_keys/

# on the server register using that info
sudo subscription-manager register --org={org ID} --activationkey={the name of the system}
sudo subscription-manager register --org=16178406 --activationkey=xps15

# unregister a system
sudo subscription-manager remove --all
sudo subscription-manager unregister
sudo subscription-manager clean

