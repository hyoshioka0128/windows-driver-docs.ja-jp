---
title: デバイス マネージャーのエラー メッセージ
description: デバイス マネージャーのエラー メッセージ
ms.assetid: 38958790-6b60-48ff-a341-fc39a16602ab
keywords:
- デバイスマネージャー WDK、エラー
- エラー WDK デバイスマネージャー
- 黄色い感嘆符 (WDK デバイスマネージャー)
- メッセージ WDK デバイスマネージャー
ms.date: 03/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 64860e5c5c0c53c8d723be5738243b61ab92df18
ms.sourcegitcommit: 1c9663adcbcb23167c5f2a10b36963e5d5c25c99
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2020
ms.locfileid: "78289777"
---
# <a name="device-manager-error-messages"></a>デバイス マネージャーのエラー メッセージ





デバイスに黄色い感嘆符をマークするとデバイスマネージャーエラーメッセージも表示されます。

次の表に、デバイスマネージャーによって報告されるエラーを示します。 これらのエラーコードは、Cfg で定義されています。
 
関連情報については、「[デバイスインスタンスの状態と問題コードの取得](retrieving-the-status-and-problem-code-for-a-device-instance.md)」を参照してください。


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エラー コード</th>
<th align="left">問題の名前</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>コード1</p></td>
<td align="left"><p><a href="cm-prob-not-configured.md" data-raw-source="[CM_PROB_NOT_CONFIGURED](cm-prob-not-configured.md)">CM_PROB_NOT_CONFIGURED</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード3</p></td>
<td align="left"><p><a href="cm-prob-out-of-memory.md" data-raw-source="[CM_PROB_OUT_OF_MEMORY](cm-prob-out-of-memory.md)">CM_PROB_OUT_OF_MEMORY</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード9</p></td>
<td align="left"><p><a href="cm-prob-invalid-data.md" data-raw-source="[CM_PROB_INVALID_DATA](cm-prob-invalid-data.md)">CM_PROB_INVALID_DATA</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード10</p></td>
<td align="left"><p><a href="cm-prob-failed-start.md" data-raw-source="[CM_PROB_FAILED_START](cm-prob-failed-start.md)">CM_PROB_FAILED_START</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード12</p></td>
<td align="left"><p><a href="cm-prob-normal-conflict.md" data-raw-source="[CM_PROB_NORMAL_CONFLICT](cm-prob-normal-conflict.md)">CM_PROB_NORMAL_CONFLICT</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード14</p></td>
<td align="left"><p><a href="cm-prob-need-restart.md" data-raw-source="[CM_PROB_NEED_RESTART](cm-prob-need-restart.md)">CM_PROB_NEED_RESTART</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード16</p></td>
<td align="left"><p><a href="cm-prob-partial-log-conf.md" data-raw-source="[CM_PROB_PARTIAL_LOG_CONF](cm-prob-partial-log-conf.md)">CM_PROB_PARTIAL_LOG_CONF</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード18</p></td>
<td align="left"><p><a href="cm-prob-reinstall.md" data-raw-source="[CM_PROB_REINSTALL](cm-prob-reinstall.md)">CM_PROB_REINSTALL</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード19</p></td>
<td align="left"><p><a href="cm-prob-registry.md" data-raw-source="[CM_PROB_REGISTRY](cm-prob-registry.md)">CM_PROB_REGISTRY</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード21</p></td>
<td align="left"><p><a href="cm-prob-will-be-removed.md" data-raw-source="[CM_PROB_WILL_BE_REMOVED](cm-prob-will-be-removed.md)">CM_PROB_WILL_BE_REMOVED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード22</p></td>
<td align="left"><p><a href="cm-prob-disabled.md" data-raw-source="[CM_PROB_DISABLED](cm-prob-disabled.md)">CM_PROB_DISABLED</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード24</p></td>
<td align="left"><p><a href="cm-prob-device-not-there.md" data-raw-source="[CM_PROB_DEVICE_NOT_THERE](cm-prob-device-not-there.md)">CM_PROB_DEVICE_NOT_THERE</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード28</p></td>
<td align="left"><p><a href="cm-prob-failed-install.md" data-raw-source="[CM_PROB_FAILED_INSTALL](cm-prob-failed-install.md)">CM_PROB_FAILED_INSTALL</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード29</p></td>
<td align="left"><p><a href="cm-prob-hardware-disabled.md" data-raw-source="[CM_PROB_HARDWARE_DISABLED](cm-prob-hardware-disabled.md)">CM_PROB_HARDWARE_DISABLED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード31</p></td>
<td align="left"><p><a href="cm-prob-failed-add.md" data-raw-source="[CM_PROB_FAILED_ADD](cm-prob-failed-add.md)">CM_PROB_FAILED_ADD</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード32</p></td>
<td align="left"><p><a href="cm-prob-disabled-service.md" data-raw-source="[CM_PROB_DISABLED_SERVICE](cm-prob-disabled-service.md)">CM_PROB_DISABLED_SERVICE</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード33</p></td>
<td align="left"><p><a href="cm-prob-translation-failed.md" data-raw-source="[CM_PROB_TRANSLATION_FAILED](cm-prob-translation-failed.md)">CM_PROB_TRANSLATION_FAILED</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード34</p></td>
<td align="left"><p><a href="cm-prob-no-softconfig.md" data-raw-source="[CM_PROB_NO_SOFTCONFIG](cm-prob-no-softconfig.md)">CM_PROB_NO_SOFTCONFIG</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード35</p></td>
<td align="left"><p><a href="cm-prob-bios-table.md" data-raw-source="[CM_PROB_BIOS_TABLE](cm-prob-bios-table.md)">CM_PROB_BIOS_TABLE</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード36</p></td>
<td align="left"><p><a href="cm-prob-irq-translation-failed.md" data-raw-source="[CM_PROB_IRQ_TRANSLATION_FAILED](cm-prob-irq-translation-failed.md)">CM_PROB_IRQ_TRANSLATION_FAILED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード37</p></td>
<td align="left"><p><a href="cm-prob-failed-driver-entry.md" data-raw-source="[CM_PROB_FAILED_DRIVER_ENTRY](cm-prob-failed-driver-entry.md)">CM_PROB_FAILED_DRIVER_ENTRY</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード38</p></td>
<td align="left"><p><a href="cm-prob-driver-failed-prior-unload.md" data-raw-source="[CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD](cm-prob-driver-failed-prior-unload.md)">CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Code 39</p></td>
<td align="left"><p><a href="cm-prob-driver-failed-load.md" data-raw-source="[CM_PROB_DRIVER_FAILED_LOAD](cm-prob-driver-failed-load.md)">CM_PROB_DRIVER_FAILED_LOAD</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード40</p></td>
<td align="left"><p><a href="cm-prob-driver-service-key-invalid.md" data-raw-source="[CM_PROB_DRIVER_SERVICE_KEY_INVALID](cm-prob-driver-service-key-invalid.md)">CM_PROB_DRIVER_SERVICE_KEY_INVALID</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード41</p></td>
<td align="left"><p><a href="cm-prob-legacy-service-no-devices.md" data-raw-source="[CM_PROB_LEGACY_SERVICE_NO_DEVICES](cm-prob-legacy-service-no-devices.md)">CM_PROB_LEGACY_SERVICE_NO_DEVICES</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード42</p></td>
<td align="left"><p><a href="cm-prob-duplicate-device.md" data-raw-source="[CM_PROB_DUPLICATE_DEVICE](cm-prob-duplicate-device.md)">CM_PROB_DUPLICATE_DEVICE</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード43</p></td>
<td align="left"><p><a href="cm-prob-failed-post-start.md" data-raw-source="[CM_PROB_FAILED_POST_START](cm-prob-failed-post-start.md)">CM_PROB_FAILED_POST_START</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード44</p></td>
<td align="left"><p><a href="cm-prob-halted.md" data-raw-source="[CM_PROB_HALTED](cm-prob-halted.md)">CM_PROB_HALTED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード45</p></td>
<td align="left"><p><a href="cm-prob-phantom.md" data-raw-source="[CM_PROB_PHANTOM](cm-prob-phantom.md)">CM_PROB_PHANTOM</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード46</p></td>
<td align="left"><p><a href="cm-prob-system-shutdown.md" data-raw-source="[CM_PROB_SYSTEM_SHUTDOWN](cm-prob-system-shutdown.md)">CM_PROB_SYSTEM_SHUTDOWN</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード47</p></td>
<td align="left"><p><a href="cm-prob-held-for-eject.md" data-raw-source="[CM_PROB_HELD_FOR_EJECT](cm-prob-held-for-eject.md)">CM_PROB_HELD_FOR_EJECT</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード48</p></td>
<td align="left"><p><a href="cm-prob-driver-blocked.md" data-raw-source="[CM_PROB_DRIVER_BLOCKED](cm-prob-driver-blocked.md)">CM_PROB_DRIVER_BLOCKED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード49</p></td>
<td align="left"><p><a href="cm-prob-registry-too-large.md" data-raw-source="[CM_PROB_REGISTRY_TOO_LARGE](cm-prob-registry-too-large.md)">CM_PROB_REGISTRY_TOO_LARGE</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード50</p></td>
<td align="left"><p><a href="cm-prob-setproperties-failed.md" data-raw-source="[CM_PROB_SETPROPERTIES_FAILED](cm-prob-setproperties-failed.md)">CM_PROB_SETPROPERTIES_FAILED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード51</p></td>
<td align="left"><p><a href="cm-prob-waiting-on-dependency.md" data-raw-source="[CM_PROB_WAITING_ON_DEPENDENCY](cm-prob-waiting-on-dependency.md)">CM_PROB_WAITING_ON_DEPENDENCY</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード52</p></td>
<td align="left"><p><a href="cm-prob-unsigned-driver.md" data-raw-source="[CM_PROB_UNSIGNED_DRIVER](cm-prob-unsigned-driver.md)">CM_PROB_UNSIGNED_DRIVER</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード53</p></td>
<td align="left"><p><a href="cm-prob-used-by-debugger.md" data-raw-source="[CM_PROB_USED_BY_DEBUGGER](cm-prob-used-by-debugger.md)">CM_PROB_USED_BY_DEBUGGER</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード54</p></td>
<td align="left"><p><a href="cm-prob-device-reset.md" data-raw-source="[CM_PROB_DEVICE_RESET](cm-prob-device-reset.md)">CM_PROB_DEVICE_RESET</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード55</p></td>
<td align="left"><p><a href="cm-prob-console-locked.md" data-raw-source="[CM_PROB_CONSOLE_LOCKED](cm-prob-console-locked.md)">CM_PROB_CONSOLE_LOCKED</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード56</p></td>
<td align="left"><p><a href="cm-prob-need-class-config.md" data-raw-source="[CM_PROB_NEED_CLASS_CONFIG](cm-prob-need-class-config.md)">CM_PROB_NEED_CLASS_CONFIG</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード57</p></td>
<td align="left"><p><a href="cm-prob-guest-assignment-failed.md" data-raw-source="[CM_PROB_GUEST_ASSIGNMENT_FAILED](cm-prob-guest-assignment-failed.md)">CM_PROB_GUEST_ASSIGNMENT_FAILED</a></p></td>
</tr>
</tbody>
</table>

 

 

 





