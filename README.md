<!-- anashost_support_badges_start -->
[![PayPal.Me][paypal_me_shield]][paypal_me]
[![Revolut.Me][revolut_me_shield]][revolut_me]
[![ko_fi][ko_fi_shield]][ko_fi_me]
<!-- anashost_support_badges_end -->

# HA-CAMERA-KEYPAD

### create the folowing:
`alarm_control_panel.unlock_camera` [how?](https://www.home-assistant.io/integrations/manual/)

 <details>
   <summary>my alarm sensor configs</summary>
  
```
  - platform: manual
    name: unlock Camera
    code: "1234"
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

<details>
  <summary>keypad card</summary>

```
type: conditional
conditions:
  - entity: alarm_control_panel.unlock_camera
    state: armed_away
card:
  type: custom:mushroom-alarm-control-panel-card
  entity: alarm_control_panel.unlock_camera
  states:
    - armed_away
  double_tap_action:
    action: none
  hold_action:
    action: none
  tap_action:
    action: none
  show_keypad: true
  primary_info: name
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
