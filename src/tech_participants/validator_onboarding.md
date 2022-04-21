# Validator Onboarding

* ["Onboard - Easy Mode" onboard CLI](https://github.com/OLSF/libra/blob/main/ol/documentation/node-ops/validators/validator_onboarding_easy_mode.md)
* ["Onboard - Hard Mode" discrete steps](https://github.com/OLSF/libra/blob/main/ol/documentation/node-ops/validators/validator_onboarding_hard_mode.md)
  - [old onboarding instructions](https://github.com/roamingrabbit/libra/blob/rr-update-validator-setup-docs/ol/documentation/validator_setup.md)
```console
$ RUST_LOG=error diem-node -f ~/.0L/validator.node.yaml >> ~/.0L/logs/validator.log 2>&1
```
web server
```console
$ ol serve --update
$ ol serve -c >> ~/.0L/logs/web.log 2>&1
```

