# Anti-Recovery Android Bootloader

Based on the EFI Development Kit II (EDKII / EDK2), the anti-recovery Android bootloader prevents the scenarios that the edge computing devices running Android stuck on the recovery mode (e.g. Rescue Party, file-based encryption errors).

## Covered Scenarios

The edge computing devices are triggered to reboot into recovery mode by:

### Command `adb reboot recovery`

| Name             | Value               |
| :--------------- | :------------------ |
| Solution         | bypass              |
| BootReason       | 1                   |
| BootIntoRecovery | 0                   |
| Msg->command     | bootonce-bootloader |
| Msg->recovery    |                     |

### Command `fastboot reboot recovery`

| Name             | Value         |
| :--------------- | :------------ |
| Solution         | bypass        |
| BootReason       | 0             |
| BootIntoRecovery | 1             |
| Msg->command     | boot-recovery |
| Msg->recovery    |               |

### File-Based Encryption (FBE) Errors

| Name             | Value                                                                 |
| :--------------- | :-------------------------------------------------------------------- |
| Solution         | bypass                                                                |
| BootReason       | 0                                                                     |
| BootIntoRecovery | 1                                                                     |
| Msg->command     | boot-recovery                                                         |
| Msg->recovery    | recovery --prompt_and_wipe_data --reason=set_policy_failed:/data/fota |
