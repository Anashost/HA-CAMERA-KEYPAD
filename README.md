# HA-CAMERA-KEYPAD
automation:
`
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

`
