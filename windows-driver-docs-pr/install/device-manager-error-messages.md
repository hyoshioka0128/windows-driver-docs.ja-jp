---
title: デバイス マネージャーのエラー メッセージ
description: デバイス マネージャーのエラー メッセージ
ms.assetid: 38958790-6b60-48ff-a341-fc39a16602ab
keywords:
- デバイス マネージャーの WDK、エラー
- WDK デバイス マネージャーのエラー
- 黄色の感嘆符 WDK デバイス マネージャー
- WDK デバイス マネージャー メッセージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cc82a6dd9c6b5a9776e5e4878e762f8da54c97a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557239"
---
# <a name="device-manager-error-messages"></a>デバイス マネージャーのエラー メッセージ





デバイス マネージャーは、黄色の感嘆符を使用したデバイスをマーク、ときにも、エラー メッセージを提供します。

次の表では、デバイス マネージャーによって報告されたエラーを示します。 これらのエラー コードは、Cfg.h で定義されます。

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
<td align="left"><p>コード 1</p></td>
<td align="left"><p><a href="cm-prob-not-configured.md" data-raw-source="[CM_PROB_NOT_CONFIGURED](cm-prob-not-configured.md)">CM_PROB_NOT_CONFIGURED</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 3</p></td>
<td align="left"><p><a href="cm-prob-out-of-memory.md" data-raw-source="[CM_PROB_OUT_OF_MEMORY](cm-prob-out-of-memory.md)">CM_PROB_OUT_OF_MEMORY</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 9</p></td>
<td align="left"><p><a href="cm-prob-invalid-data.md" data-raw-source="[CM_PROB_INVALID_DATA](cm-prob-invalid-data.md)">CM_PROB_INVALID_DATA</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 10</p></td>
<td align="left"><p><a href="cm-prob-failed-start.md" data-raw-source="[CM_PROB_FAILED_START](cm-prob-failed-start.md)">CM_PROB_FAILED_START</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 12</p></td>
<td align="left"><p><a href="cm-prob-normal-conflict.md" data-raw-source="[CM_PROB_NORMAL_CONFLICT](cm-prob-normal-conflict.md)">CM_PROB_NORMAL_CONFLICT</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 14</p></td>
<td align="left"><p><a href="cm-prob-need-restart.md" data-raw-source="[CM_PROB_NEED_RESTART](cm-prob-need-restart.md)">CM_PROB_NEED_RESTART</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Code 16</p></td>
<td align="left"><p><a href="cm-prob-partial-log-conf.md" data-raw-source="[CM_PROB_PARTIAL_LOG_CONF](cm-prob-partial-log-conf.md)">CM_PROB_PARTIAL_LOG_CONF</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 18</p></td>
<td align="left"><p><a href="cm-prob-reinstall.md" data-raw-source="[CM_PROB_REINSTALL](cm-prob-reinstall.md)">CM_PROB_REINSTALL</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コードの 19</p></td>
<td align="left"><p><a href="cm-prob-registry.md" data-raw-source="[CM_PROB_REGISTRY](cm-prob-registry.md)">CM_PROB_REGISTRY</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 21</p></td>
<td align="left"><p><a href="cm-prob-will-be-removed.md" data-raw-source="[CM_PROB_WILL_BE_REMOVED](cm-prob-will-be-removed.md)">CM_PROB_WILL_BE_REMOVED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 22</p></td>
<td align="left"><p><a href="cm-prob-disabled.md" data-raw-source="[CM_PROB_DISABLED](cm-prob-disabled.md)">CM_PROB_DISABLED</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 24</p></td>
<td align="left"><p><a href="cm-prob-device-not-there.md" data-raw-source="[CM_PROB_DEVICE_NOT_THERE](cm-prob-device-not-there.md)">CM_PROB_DEVICE_NOT_THERE</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 28</p></td>
<td align="left"><p><a href="cm-prob-failed-install.md" data-raw-source="[CM_PROB_FAILED_INSTALL](cm-prob-failed-install.md)">CM_PROB_FAILED_INSTALL</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 29</p></td>
<td align="left"><p><a href="cm-prob-hardware-disabled.md" data-raw-source="[CM_PROB_HARDWARE_DISABLED](cm-prob-hardware-disabled.md)">CM_PROB_HARDWARE_DISABLED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 31</p></td>
<td align="left"><p><a href="cm-prob-failed-add.md" data-raw-source="[CM_PROB_FAILED_ADD](cm-prob-failed-add.md)">CM_PROB_FAILED_ADD</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 32</p></td>
<td align="left"><p><a href="cm-prob-disabled-service.md" data-raw-source="[CM_PROB_DISABLED_SERVICE](cm-prob-disabled-service.md)">CM_PROB_DISABLED_SERVICE</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 33</p></td>
<td align="left"><p><a href="cm-prob-translation-failed.md" data-raw-source="[CM_PROB_TRANSLATION_FAILED](cm-prob-translation-failed.md)">CM_PROB_TRANSLATION_FAILED</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 34</p></td>
<td align="left"><p><a href="cm-prob-no-softconfig.md" data-raw-source="[CM_PROB_NO_SOFTCONFIG](cm-prob-no-softconfig.md)">CM_PROB_NO_SOFTCONFIG</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 35</p></td>
<td align="left"><p><a href="cm-prob-bios-table.md" data-raw-source="[CM_PROB_BIOS_TABLE](cm-prob-bios-table.md)">CM_PROB_BIOS_TABLE</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 36</p></td>
<td align="left"><p><a href="cm-prob-irq-translation-failed.md" data-raw-source="[CM_PROB_IRQ_TRANSLATION_FAILED](cm-prob-irq-translation-failed.md)">CM_PROB_IRQ_TRANSLATION_FAILED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 37</p></td>
<td align="left"><p><a href="cm-prob-failed-driver-entry.md" data-raw-source="[CM_PROB_FAILED_DRIVER_ENTRY](cm-prob-failed-driver-entry.md)">CM_PROB_FAILED_DRIVER_ENTRY</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 38</p></td>
<td align="left"><p><a href="cm-prob-driver-failed-prior-unload.md" data-raw-source="[CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD](cm-prob-driver-failed-prior-unload.md)">CM_PROB_DRIVER_FAILED_PRIOR_UNLOAD</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Code 39</p></td>
<td align="left"><p><a href="cm-prob-driver-failed-load.md" data-raw-source="[CM_PROB_DRIVER_FAILED_LOAD](cm-prob-driver-failed-load.md)">CM_PROB_DRIVER_FAILED_LOAD</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 40</p></td>
<td align="left"><p><a href="cm-prob-driver-service-key-invalid.md" data-raw-source="[CM_PROB_DRIVER_SERVICE_KEY_INVALID](cm-prob-driver-service-key-invalid.md)">CM_PROB_DRIVER_SERVICE_KEY_INVALID</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 41</p></td>
<td align="left"><p><a href="cm-prob-legacy-service-no-devices.md" data-raw-source="[CM_PROB_LEGACY_SERVICE_NO_DEVICES](cm-prob-legacy-service-no-devices.md)">CM_PROB_LEGACY_SERVICE_NO_DEVICES</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 42</p></td>
<td align="left"><p><a href="cm-prob-duplicate-device.md" data-raw-source="[CM_PROB_DUPLICATE_DEVICE](cm-prob-duplicate-device.md)">CM_PROB_DUPLICATE_DEVICE</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 43</p></td>
<td align="left"><p><a href="cm-prob-failed-post-start.md" data-raw-source="[CM_PROB_FAILED_POST_START](cm-prob-failed-post-start.md)">CM_PROB_FAILED_POST_START</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 44</p></td>
<td align="left"><p><a href="cm-prob-halted.md" data-raw-source="[CM_PROB_HALTED](cm-prob-halted.md)">CM_PROB_HALTED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 45</p></td>
<td align="left"><p><a href="cm-prob-phantom.md" data-raw-source="[CM_PROB_PHANTOM](cm-prob-phantom.md)">CM_PROB_PHANTOM</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 46</p></td>
<td align="left"><p><a href="cm-prob-system-shutdown.md" data-raw-source="[CM_PROB_SYSTEM_SHUTDOWN](cm-prob-system-shutdown.md)">CM_PROB_SYSTEM_SHUTDOWN</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 47</p></td>
<td align="left"><p><a href="cm-prob-held-for-eject.md" data-raw-source="[CM_PROB_HELD_FOR_EJECT](cm-prob-held-for-eject.md)">CM_PROB_HELD_FOR_EJECT</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 48</p></td>
<td align="left"><p><a href="cm-prob-driver-blocked.md" data-raw-source="[CM_PROB_DRIVER_BLOCKED](cm-prob-driver-blocked.md)">CM_PROB_DRIVER_BLOCKED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 49</p></td>
<td align="left"><p><a href="cm-prob-registry-too-large.md" data-raw-source="[CM_PROB_REGISTRY_TOO_LARGE](cm-prob-registry-too-large.md)">CM_PROB_REGISTRY_TOO_LARGE</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 50</p></td>
<td align="left"><p><a href="cm-prob-setproperties-failed.md" data-raw-source="[CM_PROB_SETPROPERTIES_FAILED](cm-prob-setproperties-failed.md)">CM_PROB_SETPROPERTIES_FAILED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 51</p></td>
<td align="left"><p><a href="cm-prob-waiting-on-dependency.md" data-raw-source="[CM_PROB_WAITING_ON_DEPENDENCY](cm-prob-waiting-on-dependency.md)">CM_PROB_WAITING_ON_DEPENDENCY</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 52</p></td>
<td align="left"><p><a href="cm-prob-unsigned-driver.md" data-raw-source="[CM_PROB_UNSIGNED_DRIVER](cm-prob-unsigned-driver.md)">CM_PROB_UNSIGNED_DRIVER</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>コード 53</p></td>
<td align="left"><p><a href="cm-prob-used-by-debugger.md" data-raw-source="[CM_PROB_USED_BY_DEBUGGER](cm-prob-used-by-debugger.md)">CM_PROB_USED_BY_DEBUGGER</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>コード 54</p></td>
<td align="left"><p><a href="cm-prob-device-reset.md" data-raw-source="[CM_PROB_DEVICE_RESET](cm-prob-device-reset.md)">CM_PROB_DEVICE_RESET</a></p></td>
</tr>
</tbody>
</table>

 

 

 





