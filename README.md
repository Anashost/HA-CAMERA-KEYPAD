<!-- anashost_support_badges_start -->
[![PayPal.Me][paypal_me_shield]][paypal_me]
[![Revolut.Me][revolut_me_shield]][revolut_me]
[![ko_fi][ko_fi_shield]][ko_fi_me]
<!-- anashost_support_badges_end -->

# HA-CAMERA-KEYPAD

### create the folowing:
- `alarm_control_panel.unlock_camera` [how?](https://www.home-assistant.io/integrations/manual/)

 <details>
   <summary>my alarm sensor configs</summary>
  
```
  - platform: manual
    name: unlock Camera
    code: !secret camera_code
    code_arm_required: false
    arming_time: 0.5
    delay_time: 0.5
    trigger_time: 5
    disarmed:
      trigger_time: 0
    armed_home:
      arming_time: 0
      delay_time: 0
```

</details>

- `input_boolean.show_cam_keypad` *from helpers*

<details>
  <summary>keypad card</summary>

```
type: conditional
conditions:
  - entity: input_boolean.show_cam_keypad
    state: 'on'
card:
  type: alarm-panel
  states:
    - arm_away
  entity: alarm_control_panel.unlock_camera
  name: Unlock Camera

```
</details>

<details>
  <summary>camera card</summary>
 - replace camera.xxx with your camera entity.
  
```
type: conditional
conditions:
  - entity: alarm_control_panel.unlock_camera
    state: disarmed
card:
  camera_view: live
  type: picture-glance
  entities: []
  aspect_ratio: 55%
  camera_image: camera.xxx
  theme: Mushroom Shadow
  hold_action:
    action: none
```
</details>

<details>
  <summary>automation</summary>

```
alias: cam view toggle - keypad
description: ""
trigger:
  - platform: state
    entity_id:
      - alarm_control_panel.unlock_camera
    from: arming
    to: armed_away
    id: arm
    for:
      hours: 0
      minutes: 0
      seconds: 0
  - platform: state
    entity_id:
      - alarm_control_panel.unlock_camera
    from:
      - armed_away
      - armed_vacation
      - armed_night
      - armed_custom_bypass
      - armed_home
      - disarming
    to: disarmed
    id: disarm
condition: []
action:
  - choose:
      - conditions:
          - condition: trigger
            id:
              - disarm
        sequence:
          - service: input_boolean.turn_off
            data: {}
            target:
              entity_id: input_boolean.show_cam_keypad
      - conditions:
          - condition: trigger
            id:
              - arm
        sequence:
          - service: input_boolean.turn_on
            data: {}
            target:
              entity_id: input_boolean.show_cam_keypad
mode: single
```

</details>

[latest_release]: https://github.com/Anashost/MY-HA-DASH/releases/latest

[releases_shield]: https://img.shields.io/github/release/Anashost/MY-HA-DASH.svg?style=popout

[releases]: https://github.com/Anashost/MY-HA-DASH/releases

[downloads_total_shield]: https://img.shields.io/github/downloads/Anashost/MY-HA-DASH/total

[community_forum_shield]: https://img.shields.io/static/v1.svg?label=%20&message=Forum&style=popout&color=41bdf5&logo=HomeAssistant&logoColor=white

[community_forum]: https://github.com/Anashost/MY-HA-DASH/issues

[paypal_me_shield]: https://img.shields.io/static/v1.svg?label=%20&message=PayPal&logo=paypal

[paypal_me]: https://www.paypal.me/anashost

[revolut_me_shield]: https://img.shields.io/static/v1.svg?label=%20&message=Revolut&logo=revolut

[revolut_me]: https://revolut.me/anas4e

[ko_fi_shield]: https://img.shields.io/static/v1.svg?label=%20&message=ByMeCoffee&logo=ko-fi

[ko_fi_me]: https://ko-fi.com/anasbox
