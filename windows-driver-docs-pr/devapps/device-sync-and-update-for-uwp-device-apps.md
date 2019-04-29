---
title: デバイスとの同期と Windows 8.1 のストア デバイス アプリ用の更新プログラム
description: Windows 8.1 では、UWP アプリは、デバイス バックグラウンド タスクを使用して、周辺機器上のデータを同期できます。
ms.assetid: AA6E0760-F048-4BDC-8429-D119A531CED6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad38e4fc6ca929f5323d0fe6abe064e7096d6431
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391370"
---
# <a name="device-sync-and-update-for-store-device-apps-in-windows-81"></a>デバイスとの同期と Windows 8.1 のストア デバイス アプリ用の更新プログラム


Windows 8.1 では、UWP アプリは、デバイス バックグラウンド タスクを使用して、周辺機器上のデータを同期できます。 アプリがデバイス メタデータに関連付けられている場合、その UWP デバイス アプリは、デバイス バック グラウンド エージェントを使用して、ファームウェアの更新などのデバイスの更新を実行することもできます。 デバイスのバック グラウンド エージェントは、同期され更新されているユーザーの同意を確認し、デバイスは、バッテリの寿命を保てるようにするポリシーが適用されます。

デバイスとの同期を実行し、更新操作、使用するデバイスのバック グラウンド タスクを作成、 [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)と[DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)、それぞれします。 これを行う方法については、[カスタム USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=301975 )と[ファームウェア更新の USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=309186)を参照してください[デバイスのバック グラウンド タスクを作成する](how-to-create-a-device-background-task.md)します。

**注**  デバイスの Windows ランタイム Api は、デバイスのメタデータを必要としません。 つまり、アプリは、それらを使用するデバイス アプリを UWP をする必要はありません。 UWP アプリでは、USB、ヒューマン インターフェイス デバイス (HID)、Bluetooth デバイス、およびアクセスをこれらの Api を使用できます。 詳細については、次を参照してください。[デバイス統合](https://go.microsoft.com/fwlink/p/?LinkId=533279)します。

 

## <a name="span-iddevicebackgroundtaskoverviewspanspan-iddevicebackgroundtaskoverviewspanspan-iddevicebackgroundtaskoverviewspandevice-background-task-overview"></a><span id="Device_background_task_overview_"></span><span id="device_background_task_overview_"></span><span id="DEVICE_BACKGROUND_TASK_OVERVIEW_"></span>デバイスのバック グラウンド タスクの概要


ユーザーは、画面外の UWP アプリを移動するときに、Windows には、アプリでメモリが中断します。 これには、別のアプリがフォア グラウンドがあることができます。 アプリが中断されるは、メモリ内の常駐は、Windows が実行を停止しました。 この場合、デバイスのバック グラウンド タスクを使用しない限り、同期や更新などの任意の継続的なデバイス操作が中断されます。 Windows 8.1 には、アプリが中断されている場合でも、アプリがバック グラウンドで安全に周辺機器デバイスで実行時間の長い同期と更新の操作を実行する 2 つの新しいバック グラウンド タスク トリガーが用意されています。DeviceUseTrigger DeviceServicingTrigger. アプリの中断に関する詳細については、次を参照してください。 [Launching, resuming, とマルチタスク](https://go.microsoft.com/fwlink/p/?LinkId=309316)します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">バック グラウンド タスクのトリガー</th>
<th align="left">デバイス メタデータが必要です。</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?LinkID=308967" data-raw-source="[DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)">DeviceUseTrigger</a></td>
<td align="left"></td>
<td align="left">アプリが中断されている間、周辺機器のデバイスに同期操作を実行時間の長い有効にします。 バック グラウンドで、デバイスを同期するには、アプリでバック グラウンドの同期中、ユーザーが承認することが必要です。 デバイスに接続されているまたは作業中の i/o、PC とペアリングもする必要がありますが、最大 10 分間のバック グラウンド アクティビティが許可されます。 ポリシーの適用については、このトピックの後半で詳しく説明します。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?LinkID=308965" data-raw-source="[DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)">DeviceServicingTrigger</a></td>
<td align="left"><img src="images/ap-tools.png" alt="DeviceServicingTrigger requires device metadata." /></td>
<td align="left">デバイスの更新プログラムの実行時間の長い有効では、設定の転送やファームウェアを更新、アプリが中断されている間します。 バック グラウンドでデバイスを更新すると、バック グラウンド タスクが使用されるたびにユーザーの承認が必要です。 DeviceUseTrigger バック グラウンド タスクとは異なりは、DeviceServicingTrigger バック グラウンド タスクはデバイスの再起動により、切断とにより、バック グラウンド アクティビティの 30 分の最大数。 ポリシーの適用については、このトピックの後半で詳しく説明します。</td>
</tr>
</tbody>
</table>

 

DeviceServicingTrigger では、デバイスの更新操作を実行するために特権を持つアプリとしてアプリを指定する必要がありますので、デバイスのメタデータが必要です。

### <a name="span-idappprivilegespanspan-idappprivilegespanspan-idappprivilegespanapp-privilege"></a><span id="App_privilege"></span><span id="app_privilege"></span><span id="APP_PRIVILEGE"></span>アプリの権限

デバイスの更新プログラムが実行時間の長いなど、一部の不可欠なデバイス操作は、特権のあるアプリでのみ実行できます。 A*特権を持つアプリ*はこれらの操作を実行するデバイスの製造元が承認されているアプリです。 デバイス メタデータは、どのアプリでは、存在する場合と指定されたデバイスの特権を持つアプリを指定します。

デバイス メタデータのウィザードを使用して、デバイスのメタデータを作成するときにで、アプリを指定、**指定 UWP デバイスのアプリ情報**ページ。 詳細については、次を参照してください。[手順 2。デバイス メタデータ、UWP デバイス アプリを作成](step-2--create-device-metadata.md)です。

## <a name="span-idsupportedprotocolsspanspan-idsupportedprotocolsspanspan-idsupportedprotocolsspansupported-protocols"></a><span id="Supported_protocols"></span><span id="supported_protocols"></span><span id="SUPPORTED_PROTOCOLS"></span>サポートされているプロトコル


DeviceUseTrigger と DeviceServicingTrigger を使用するデバイスのバック グラウンド タスクは、周辺機器と UWP アプリで通常使用されるシステムによってトリガーされるタスクでサポートされていないプロトコル経由の通信、アプリを使用できます。

| プロトコル         | DeviceServicingTrigger                                                   | DeviceUseTrigger                                                                         | システムのトリガー                                                                       |
|------------------|--------------------------------------------------------------------------|------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| USB              | ![deviceservicingtrigger usb をサポートしています](images/ap-tools.png)              | ![deviceusetrigger usb をサポートしています](images/ap-tools.png)                                    | ![システムのトリガーは usb をサポートしていません](images/app-tools-doesnotapply.png)              |
| HID              | ![hid deviceservicingtrigger サポート](images/ap-tools.png)              | ![hid deviceusetrigger サポート](images/ap-tools.png)                                    | ![システムのトリガーをサポートしていない非表示](images/app-tools-doesnotapply.png)              |
| Bluetooth RFCOMM | ![deviceservicingtrigger は、bluetooth rfcomm をサポートしています](images/ap-tools.png) | ![deviceusetrigger は、bluetooth rfcomm をサポートしています](images/ap-tools.png)                       | ![システムのトリガーは bluetooth rfcomm をサポートしていません](images/app-tools-doesnotapply.png) |
| Bluetooth GATT   | ![bluetooth をサポートする deviceservicingtrigger gatt](images/ap-tools.png)   | ![bluetooth をサポートする deviceusetrigger gatt](images/ap-tools.png)                         | ![システムのトリガーは bluetooth をサポートしていません gatt](images/app-tools-doesnotapply.png)   |
| MTP              | ![deviceservicingtrigger mtp をサポートしています](images/ap-tools.png)              | ![deviceusetrigger は mtp をサポートしていません](images/app-tools-doesnotapply.png)              | ![システムのトリガーは mtp をサポートしていません](images/app-tools-doesnotapply.png)              |
| ネットワーク (有線)    | ![deviceservicingtrigger は、ワイヤード (有線) ネットワークをサポートしています](images/ap-tools.png)    | ![deviceusetrigger がワイヤード (有線) ネットワークをサポートしていません](images/app-tools-doesnotapply.png)    | ![システムのトリガーはワイヤード (有線) ネットワークをサポートしていません](images/app-tools-doesnotapply.png)    |
| ネットワーク (Wi-Fi)    | ![deviceservicingtrigger は、ネットワーク、wi-fi をサポートしています。](images/ap-tools.png)  | ![deviceusetrigger がネットワーク上で wi-fi をサポートしていません](images/app-tools-doesnotapply.png)  | ![システムのトリガーには、ネットワーク、wi-fi はできません。](images/app-tools-doesnotapply.png)    |
| IDeviceIOControl | ![DeviceServicingTrigger でサポートされています。](images/ap-tools.png) | ![deviceusetrigger は ideviceiocontrol をサポートしていません](images/app-tools-doesnotapply.png) | ![システムのトリガーは ideviceiocontrol をサポートしていません](images/app-tools-doesnotapply.png) |

 

## <a name="span-idregisteringbackgroundtasksintheapppackagemanifestspanspan-idregisteringbackgroundtasksintheapppackagemanifestspanspan-idregisteringbackgroundtasksintheapppackagemanifestspanregistering-background-tasks-in-the-app-package-manifest"></a><span id="Registering_background_tasks_in_the_app_package_manifest"></span><span id="registering_background_tasks_in_the_app_package_manifest"></span><span id="REGISTERING_BACKGROUND_TASKS_IN_THE_APP_PACKAGE_MANIFEST"></span>アプリのパッケージ マニフェストの登録のバック グラウンド タスク


アプリは、バックグランド タスクの一部として動作するコードで同期操作と更新操作を実行します。 このコードは、IBackgroundTask を実装する Windows ランタイム クラス (または JavaScript アプリ専用の JavaScript ページ) に埋め込まれています。 デバイスのバック グラウンド タスクを使用するには、アプリする必要がありますで宣言はシステムによってトリガーされるバック グラウンド タスクの場合と同様に、フォア グラウンド アプリのアプリ マニフェスト ファイル。

アプリ パッケージのマニフェスト ファイルのこの例では**DeviceLibrary.SyncContent**と**DeviceLibrary.UpdateFirmware**フォア グラウンド アプリからのエントリ ポイントします。 **DeviceLibrary.SyncContent**バック グラウンド タスクを使用するためのエントリ ポイントは、 [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)します。 **DeviceLibrary.UpdateFirmware**バック グラウンド タスクを使用するためのエントリ ポイントは、 [DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)します。

```XML
<Extensions>
  <Extension Category="windows.backgroundTasks" EntryPoint="DeviceLibrary.SyncContent">
    <BackgroundTasks>
      <m2:Task Type="deviceUse" /> 
    </BackgroundTasks>
  </Extension>
  <Extension Category="windows.backgroundTasks" EntryPoint="DeviceLibrary.UpdateFirmware">
    <BackgroundTasks>
      <m2:Task Type="deviceServicing" /> 
    </BackgroundTasks>
  </Extension>
</Extensions>
```

## <a name="span-idusingyourdevicewithdevicebackgroundtasksspanspan-idusingyourdevicewithdevicebackgroundtasksspanspan-idusingyourdevicewithdevicebackgroundtasksspanusing-your-device-with-device-background-tasks"></a><span id="Using_your_device_with_device_background_tasks"></span><span id="using_your_device_with_device_background_tasks"></span><span id="USING_YOUR_DEVICE_WITH_DEVICE_BACKGROUND_TASKS"></span>デバイスのバック グラウンド タスクでデバイスを使用します。


DeviceUseTrigger と DeviceServicingTrigger バック グラウンド タスクに活用するためにアプリを開発するには、この基本的な一連の手順に従います。 バック グラウンド タスクの詳細については、次を参照してください。[バック グラウンド タスクを使用してアプリをサポートしている](https://go.microsoft.com/fwlink/p/?LinkID=254337)します。

1.  アプリ マニフェストにバックグラウンド タスクを登録し、IBackgroundTask を実装する Windows ランタイム クラスまたは JavaScript アプリ専用の JavaScript ページにバックグラウンド タスク コードを埋め込みます。
2.  アプリケーションの起動時に作成および DeviceUseTrigger または DeviceServicingTrigger のいずれか、適切な種類のデバイスのトリガー オブジェクトを構成し、将来使用するためのトリガーのインスタンスを格納します。
3.  アプリは、かどうか、バック グラウンド タスク以前に登録し、そうでない場合は、デバイスのトリガーに対して登録を確認します。 このトリガーに関連付けられているタスクには条件を設定できないことに注意してください。
4.  を、アプリがバック グラウンド タスクをトリガーする必要があるときに、デバイスのトリガー オブジェクトの RequestAsync アクティブ化メソッドを呼び出します。
5.  バックグラウンド タスクは、(CPU 時間が割り当てられない) 他のシステム バックグラウンド タスクのように抑制されません。ただし、フォアグラウンド アプリの応答性を維持するため、低い優先順位で実行されます。
6.  次に Windows は、トリガー タイプに応じて、必要なポリシー (バックラウンド タスクを開始する前にユーザーの許可を得るなど) に準拠しているかどうかを検証します。
7.  Windows はシステム条件とタスクの実行時間を監視し、必要な条件を満たさなくなった場合はタスクを中止します。
8.  バックグラウンド タスクが進捗状況や完了を報告する際、登録タスクの進捗状況イベントまたは完了イベントとしてアプリに渡されます。

**重要な**  デバイスのバック グラウンド タスクを使用する場合は、これらの重要な点を検討してください。

-   DeviceUseTrigger と DeviceServicingTrigger を使用するバック グラウンド タスクをプログラムでトリガーする機能は Windows 8.1 で導入された、デバイスのバック グラウンド タスクのみに制限されています。

-   特定のポリシーは、その周辺機器を更新するときに、ユーザーの同意を確認する Windows によって適用されます。 周辺機器を同期および更新する際、バッテリ残量を維持するためのポリシーも適用されます。

-   DeviceUseTrigger と DeviceServicingTrigger を使用するバック グラウンド タスクは、バック グラウンドの時間 (ウォール クロック時間) の最大値を含む、特定のポリシー要件が満たされなくときに、Windows によってキャンセル可能性があります。 バックグラウンド タスクを使って周辺機器を操作するときは、これらのポリシー要件を考慮する必要があります。

 

**ヒント:**  これらのバック グラウンド タスクの動作方法を表示するには、サンプルをダウンロードします。 [カスタム USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=301975 )DeviceUseTrigger とデバイスの同期を実行するバック グラウンド タスクを示します。 [ファームウェア更新の USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=309186)DeviceServicingTrigger ファームウェアの更新プログラムを実行するバック グラウンド タスクを示します。

 

## <a name="span-iduserconsentspanspan-iduserconsentspanspan-iduserconsentspanuser-consent"></a><span id="User_consent"></span><span id="user_consent"></span><span id="USER_CONSENT"></span>ユーザーの同意


DeviceUseTrigger または DeviceServicingTrigger を使用する場合、Windows 8.1 は、アプリのアクセスを許可して、バック グラウンドでのコンテンツの更新を同期してデバイスにアクセスするが、ユーザーに付与することを確認するためのポリシーを適用します。 ポリシーは、同期や周辺機器の更新時のユーザーのバッテリ寿命を維持するためにも適用されます。

### <a name="span-iddevicesyncuserconsentspanspan-iddevicesyncuserconsentspanspan-iddevicesyncuserconsentspandevice-sync-user-consent"></a><span id="Device_sync_user_consent"></span><span id="device_sync_user_consent"></span><span id="DEVICE_SYNC_USER_CONSENT"></span>デバイス同期ユーザーの同意

DeviceUseTrigger を使用するバック グラウンド タスクには、バック グラウンドで同期するアプリを許可する 1 回限りのユーザーの同意が必要です。 この同意は、アプリごとのストアドと、デバイスごとのモデルです。 ユーザーがアプリへのアクセス、バック グラウンドでデバイス、アプリがフォア グラウンド アプリからデバイスのアクセスに同意したのと同じように同意するとします。

次の例では、Tailspin Toys という名前のアプリがバック グラウンドで同期するユーザーのアクセス許可を取得します。

![デバイス同期ユーザーの同意メッセージ ダイアログ](images/devicesyncuserconsent.png)

ユーザーが抱くを後で変更する場合は、アクセス許可の設定で、取り消すことができます。

![デバイスの同期アクセス許可の設定 ダイアログ](images/devicesyncapppermissions.png)

### <a name="span-iddeviceupdateuserconsentspanspan-iddeviceupdateuserconsentspanspan-iddeviceupdateuserconsentspandevice-update-user-consent"></a><span id="Device_update_user__consent"></span><span id="device_update_user__consent"></span><span id="DEVICE_UPDATE_USER__CONSENT"></span>デバイス更新プログラムのユーザーの同意

DeviceUseTrigger、DeviceServicingTrigger バック グラウンド タスクを使用して、バック グラウンド タスクを使用してユーザーを必要とするものとは異なり、バック グラウンド タスクがトリガーされるたびに同意します。 DeviceUseTrigger のように、この同意は格納されません。 これは、デバイス ファームウェアの更新プログラムに関連するリスクが高い操作とデバイスの更新プログラムに必要な時間の長い時間が原因です。 Windows ユーザーの同意を取得するだけでなく、更新プログラムの全体で接続されているデバイスを保持し、PC は課金されることを確認する警告などのデバイスの更新プログラムと、操作のおおよその実行時間に関する情報をユーザーに提供されます (場合、アプリ提供します)。

![デバイスは、ユーザーの同意メッセージ ダイアログを更新します。](images/deviceupdateuserconsent.png)

## <a name="span-idfrequencyandforegroundrestrictionsspanspan-idfrequencyandforegroundrestrictionsspanspan-idfrequencyandforegroundrestrictionsspanfrequency-and-foreground-restrictions"></a><span id="Frequency_and_foreground_restrictions"></span><span id="frequency_and_foreground_restrictions"></span><span id="FREQUENCY_AND_FOREGROUND_RESTRICTIONS"></span>頻度とフォア グラウンドの制限


アプリが操作の開始時に使用する頻度に制限はありませんが、アプリは (これには影響しませんバック グラウンド タスクの他の種類) に、1 つだけの DeviceUseTrigger または DeviceServicingTrigger のバック グラウンド タスクの操作を実行して、ことができます。アプリがフォア グラウンド中にのみ、バック グラウンド タスクを開始します。 アプリがフォア グラウンドで配置されていない、DeviceUseTrigger または DeviceServicingTrigger でバック グラウンド タスクを開始できるようにはありません。 アプリは、最初のバック グラウンド タスクが完了する前に、2 つ目のデバイスのバック グラウンド タスクを開始できません。

## <a name="span-iddevicebackgroundtaskpoliciesspanspan-iddevicebackgroundtaskpoliciesspanspan-iddevicebackgroundtaskpoliciesspandevice-background-task-policies"></a><span id="Device_background_task_policies"></span><span id="device_background_task_policies"></span><span id="DEVICE_BACKGROUND_TASK_POLICIES"></span>デバイスのバック グラウンド タスクのポリシー


Windows は、アプリがデバイスのバック グラウンド タスクを使用しているときに、ポリシーを強制します。 これらのポリシーが満たされていない場合は、DeviceUseTrigger または DeviceServicingTrigger を使用してバック グラウンド タスクがキャンセル可能性があります。 周辺デバイスと対話するデバイスのバック グラウンド タスクを使用する場合は、これらのポリシー要件を考慮する必要があります。

### <a name="span-idtaskinitiationpoliciesspanspan-idtaskinitiationpoliciesspanspan-idtaskinitiationpoliciesspantask-initiation-policies"></a><span id="Task_initiation_policies"></span><span id="task_initiation_policies"></span><span id="TASK_INITIATION_POLICIES"></span>タスクの開始に使用ポリシー

この表では、ポリシーごとのバック グラウンド タスクのトリガーに適用するタスクの開始を示します。

| ポリシー                                                                                                                                                                                                                               | DeviceServicingTrigger                       | DeviceUseTrigger                                            |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|-------------------------------------------------------------|
| UWP アプリは、バック グラウンド タスクをトリガーすると、フォア グラウンドでは。                                                                                                                                                     | ![ポリシーが適用される](images/ap-tools.png)       | ![ポリシーが適用される](images/ap-tools.png)                      |
| デバイスは、システムに (またはワイヤレス デバイスの範囲内) にアタッチされます。                                                                                                                                                           | ![ポリシーが適用される](images/ap-tools.png)       | ![ポリシーが適用される](images/ap-tools.png)                      |
| バックグラウンド タスクは、400 ミリ秒の CPU 時間を、画面がロックされている場合は 1 分ごとに消費し (1 GHz CPU の場合)、画面がロックされていない場合は 5 分ごとに消費する。 このポリシーを満たさない場合、タスクが取り消される可能性があります。 | ![ポリシーが適用される](images/ap-tools.png)       | ![ポリシーが適用される](images/ap-tools.png)                      |
| デバイスがデバイスを使用してアプリにアクセス可能な周辺機器の Api (USB、HID、Bluetooth などの Windows ランタイム Api)。 アプリがデバイスにアクセスできない場合は、バック グラウンド タスクへのアクセスが拒否されました。                  | ![ポリシーが適用される](images/ap-tools.png)       | ![ポリシーが適用される](images/ap-tools.png)                      |
| アプリで指定されているバックグラウンド タスクのエントリ ポイントがアプリ パッケージ マニフェストに登録されている。                                                                                                                                           | ![ポリシーが適用される](images/ap-tools.png)       | ![ポリシーが適用される](images/ap-tools.png)                      |
| 継続タスクのアクセス許可が、ユーザーに付与します。                                                                                                                                                                                  | いつも。                                  | 最初に、し、アプリのアクセス許可によって制御されます。             |
| アプリによって提供される推定所要時間は、30 分未満です。                                                                                                                                                                           | ![ポリシーが適用される](images/ap-tools.png)       | ![ポリシーは適用されません。](images/app-tools-doesnotapply.png) |
| アプリは、デバイスの特権を持つアプリとして指定されます。 (があるデバイス コンテナーのデバイスのメタデータで特権を持つアプリの一覧に対する完全なアプリ ID の一致。)                                                            | ![ポリシーが適用される](images/ap-tools.png)       | ![ポリシーは適用されません。](images/app-tools-doesnotapply.png) |
| コンピューターが 33% のバッテリ残容量より大きいか AC 電源。                                                                                                                                                          | ![ポリシーが適用される](images/ap-tools.png)       | ![ポリシーは適用されません。](images/app-tools-doesnotapply.png) |
| 操作の種類ごとに 1 つだけのデバイスのバック グラウンド タスクが行われています。                                                                                                                                                                       | ![ポリシー チェックが適用される](images/ap-tools.png) | ![ポリシーが適用される](images/ap-tools.png)                      |

 

### <a name="span-idruntimepolicychecksspanspan-idruntimepolicychecksspanspan-idruntimepolicychecksspanruntime-policy-checks"></a><span id="Runtime_policy_checks"></span><span id="runtime_policy_checks"></span><span id="RUNTIME_POLICY_CHECKS"></span>ポリシーのランタイム チェック

タスクがバックグラウンドで実行されるとき、Windows によって次の実行時ポリシー要件が適用されます。 いずれかの実行時要件が満たされなくなった時点で、デバイス バックグラウンド タスクが中止されます。

この表では、ポリシーごとのバック グラウンド タスクのトリガーに適用するランタイムを示します。

| ポリシー チェック                                                                                | DeviceServicingTrigger                                      | DeviceUseTrigger                             |
|---------------------------------------------------------------------------------------------|-------------------------------------------------------------|----------------------------------------------|
| 実時間の制限 (アプリがバックグラウンドでタスクを実行できる最長時間)。 | 30 分                                                  | 10 分                                   |
| デバイスは、システムに (またはワイヤレス デバイスの範囲内) にアタッチされます。                  | ![ポリシーは適用されません。](images/app-tools-doesnotapply.png) | ![ポリシー チェックが適用される](images/ap-tools.png) |
| デバイスに対して標準的な I/O を実行する (5 秒ごとに 1 I/O)。                       | ![ポリシーは適用されません。](images/app-tools-doesnotapply.png) | ![ポリシー チェックが適用される](images/ap-tools.png) |
| アプリがタスクを中止していない。                                                              | ![ポリシー チェックが適用される](images/ap-tools.png)                | ![ポリシー チェックが適用される](images/ap-tools.png) |
| アプリが終了していない。                                                                         | ![ポリシー チェックが適用される](images/ap-tools.png)                | ![ポリシー チェックが適用される](images/ap-tools.png) |

 

## <a name="span-idbestpracticesspanspan-idbestpracticesspanspan-idbestpracticesspanbest-practices"></a><span id="Best_practices"></span><span id="best_practices"></span><span id="BEST_PRACTICES"></span>ベスト プラクティス


デバイスのバック グラウンド タスクを使用する UWP デバイス アプリのベスト プラクティスを次に示します。

### <a name="span-iddevicebackgroundtaskprogrammingmodelspanspan-iddevicebackgroundtaskprogrammingmodelspanspan-iddevicebackgroundtaskprogrammingmodelspandevice-background-task-programming-model"></a><span id="Device_background_task_programming_model"></span><span id="device_background_task_programming_model"></span><span id="DEVICE_BACKGROUND_TASK_PROGRAMMING_MODEL"></span>デバイスのバック グラウンド タスクのプログラミング モデル

ユーザーがアプリを切り替えるし、フォア グラウンド アプリケーションが中断された場合、バック グラウンドで実行する、フォア グラウンド アプリから開始操作が引き続き同期またはデバイスの更新を確実にアプリから DeviceUseTrigger または DeviceServicingTrigger バック グラウンド タスクを使用してによって Windows。 このモデルに従って、バックグラウンド タスクを登録、実行、登録解除することをお勧めします。

1.  トリガーを要求する前にバックグランド タスクを登録します。

2.  進捗状況と完了のイベント ハンドラーをトリガーに関連付けます。 アプリが中断状態から復帰すると、待機中の進捗イベントまたは完了イベントが渡されます。アプリはこれらのイベントを使用して、バックグラウンド タスクの状態を判断します。

3.  それらのデバイスが開かれ、バック グラウンド タスクで使用するのには無料になるように、DeviceUseTrigger または DeviceServicingTrigger バック グラウンド タスクをトリガーするときに、任意の開いているデバイス オブジェクトを閉じます。

4.  トリガーを登録します。

5.  タスクが完了したら、バック グラウンド タスクの登録を解除します。 バック グラウンド タスクが完了したら、バック グラウンド タスクの登録を解除、デバイスを再度開くと、UWP アプリからそれを定期的に使用し、できます。

6.  バックグラウンド タスク クラスの中止イベントを登録します。 中止イベントを登録しておけば、Windows またはフォアグラウンド アプリによってバックグランド タスクが中止されたとき、バックグラウンド タスクコードからそのタスクを適切に中止できます。

7.  アプリの終了 (中断されません)、登録を解除し、実行中のタスクをキャンセルします。

    -   アプリが終了したら、登録を解除して実行中のタスクを中止します。

    -   アプリが終了すると、バックグラウンド タスクが取り消され、既存のイベント ハンドラーが既存のバックグラウンド タスクから切断されます。 これによって、バックグラウンド タスクの状態を判断できなくなります。 バックグラウンド タスクを登録解除して取り消すことで、キャンセル コードがバックグランド タスクを適切に中止できます。

**ヒント**  でこれを行う方法の詳細については、[カスタム USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=301975 )と[ファームウェア更新の USB デバイス サンプル](https://go.microsoft.com/fwlink/p/?LinkId=309186)を参照してください[作成をデバイスのバック グラウンド タスク](how-to-create-a-device-background-task.md)します。

 

### <a name="span-idcancellingabackgroundtaskspanspan-idcancellingabackgroundtaskspanspan-idcancellingabackgroundtaskspancancelling-a-background-task"></a><span id="Cancelling_a_background_task"></span><span id="cancelling_a_background_task"></span><span id="CANCELLING_A_BACKGROUND_TASK"></span>バック グラウンド タスクのキャンセル

フォア グラウンド アプリからバック グラウンドで実行するタスクをキャンセルする、BackgroundTaskRegistration で登録解除メソッドを使用して、オブジェクトを登録するか、アプリで使用する、 [DeviceUseTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308967)または[DeviceServicingTrigger](https://go.microsoft.com/fwlink/p/?LinkID=308965)バック グラウンド タスク。 BackgroundTaskRegistration を登録解除メソッドを使用して、バック グラウンド タスクの登録を解除すると、バック グラウンド タスクをキャンセルするバック グラウンド タスクのインフラストラクチャが発生します。

Unregister メソッドさらには、ブール値 true または false 値を示すために、バック グラウンド タスクのインスタンスを現在実行されている場合をキャンセルするか完了を許可せず。 詳細については、API リファレンスを参照してください。 [BackgroundTaskRegistration.Unregister](https://go.microsoft.com/fwlink/p/?LinkId=309315)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバイスのバック グラウンド タスクを作成します。](how-to-create-a-device-background-task.md)

[カスタム USB デバイスのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=301975 )

[ファームウェア更新の USB デバイスのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=309186)

[起動する、再開、およびマルチタス キング](https://go.microsoft.com/fwlink/p/?LinkId=309316)

[バック グラウンド タスクを使用してアプリをサポートしています。](https://go.microsoft.com/fwlink/p/?LinkID=254337)

 

 






