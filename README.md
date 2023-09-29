# HA-CAMERA-KEYPAD
## create the folowing:
- `alarm_control_panel.unlock_camera`
- `input_boolean.show_cam_keypad`

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
alias: S- cam view toggle - keypad
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
