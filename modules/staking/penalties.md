---
description: >-
  The rewards described earlier incentivize desired validator behaviors. The
  penalties below exist to deter unwanted validator behaviors:
---

# Penalties

### Double Signing Penalty[​](https://wiki.findora.org/docs/modules/staking/penalties#double-signing-penalty) <a href="#double-signing-penalty" id="double-signing-penalty"></a>

This penalty triggers when a validator signs two different blocks at the same time (i.e. attempts a double spend attack). If double-signing is detected, then the violating validator will be penalized with:

*   Burned FRA: burn **5%** of FRA staked at validator

    ```
    - i.e. if validator staked 100 tokens, then 5 FRA will be burned
    ```

### Unavailability Penalty[​](https://wiki.findora.org/docs/modules/staking/penalties#unavailability-penalty) <a href="#unavailability-penalty" id="unavailability-penalty"></a>

This penalty triggers when a validator is offline. Since the availability of validators to contribute to voting is critical to securing a PoS blockchain, unreliable validators must be punished when they fall below the performance. For every missing block, **0.00001%** of FRA staked at validator will be burned.&#x20;

* {% code overflow="wrap" %}
  ```
  - i.e. if validator staked 100000 tokens, then 1 FRA will be burned when this validator miss one block.
  ```
  {% endcode %}
