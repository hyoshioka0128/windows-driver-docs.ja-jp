---
title: irp の拡張機能コマンド
description: Irp の拡張機能では、I/O 要求パケット (IRP) に関する情報が表示されます。
ms.assetid: 2260255d-813b-4b89-8dbe-6ce7e5596ccf
keywords:
- IRP
- IRP
- IO 要求パケット
- Windows デバッグ irp
ms.date: 08/23/2018
topic_type:
- apiref
api_name:
- irp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 17b1e03b9936675fb38758ddc4a1d26fe622c762
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578070"
---
# <a name="irp"></a>!irp


**! Irp**拡張機能は、I/O 要求パケット (IRP) に関する情報を表示します。

```dbgcmd
!irp Address [Detail] 
```

## <a name="span-idddkirpdbgspanspan-idddkirpdbgspanparameters"></a><span id="ddk__irp_dbg"></span><span id="DDK__IRP_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
IRP の 16 進数のアドレスを指定します。

<span id="_______Detail______"></span><span id="_______detail______"></span><span id="_______DETAIL______"></span> *詳細*   
出力には、IRP の状態、そのメモリ記述子のリスト (MDL)、所有元のスレッドと、I/O スタックのすべてのスタック情報および IRP の各スタックの場所に関する情報のアドレスが含まれます場合、このパラメーターは 1 などの任意の値に含まれています、16 進数のバージョンの主要な関数のコードおよびマイナーの関数のコードを含むです。 このパラメーターを省略すると、出力には、情報の概要のみが含まれています。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)と[デバッグ中断ストーム](debugging-an-interrupt-storm.md)この拡張機能コマンドのアプリケーション。 Irp の詳細については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 メジャーおよびマイナーの関数コードの詳細については、Windows Driver Kit (WDK) ドキュメントを参照してください。 (これらのリソースできない場合がありますのいくつかの言語および国。)

このトピックで説明、IRP 構造[ **IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)します。

返される引数を含む IRP の構造体をデコードの詳細については、次のリソースを参照してください。

- E. のある Mark Russinovich、David A. Solomon Alex Ionescu、Windows の内部構造
- Windows Driver Foundation Guy Smith、小額 Orwick とドライバーの開発


<a name="remarks"></a>コメント
-------

出力も IRP が完了し、スタックの場所が処理された後どのような条件下で各スタックの場所の完了ルーチンが呼び出されることを示します。 次の 3 つの可能性があります。

<span id="________Success"></span><span id="________success"></span><span id="________SUCCESS"></span> **成功**  
IRP が"成功"のコードが完了したら、完了ルーチンが呼び出されることを示します。

<span id="________Error"></span><span id="________error"></span><span id="________ERROR"></span> **エラー**  
完了ルーチンがエラー コードで IRP が完了したときに呼び出されることを示します。

<span id="________Cancel"></span><span id="________cancel"></span><span id="________CANCEL"></span> **キャンセル**  
IRP をキャンセルしようとした場合、完了ルーチンが呼び出されることを示します。

これらの 3 つの任意の組み合わせが表示され、表示条件のいずれかが満たされている場合、完了ルーチンが呼び出されます。 直後に、適切な値が各スタックの場所に関する情報の最初の行の末尾に記載されている、**完了コンテキスト**エントリ。

Windows 10 用のこの拡張機能からの出力の例を次に示します。

```dbgcmd
0: kd> !irp ac598dc8
Irp is active with 2 stacks 1 is current (= 0xac598e38)
 No Mdl: No System Buffer: Thread 8d1c7bc0:  Irp stack trace.  
     cmd  flg cl Device   File     Completion-Context
>[IRP_MJ_FILE_SYSTEM_CONTROL(d), N/A(0)]
            1 e1 8a6434d8 ac598d40 853220cb-a89682d8 Success Error Cancel pending
           \FileSystem\Npfs fltmgr!FltpPassThroughCompletion
            Args: 00000000 00000000 00110008 00000000
 [IRP_MJ_FILE_SYSTEM_CONTROL(d), N/A(0)]
            1  0 8a799710 ac598d40 00000000-00000000    
           \FileSystem\FltMgr
            Args: 00000000 00000000 0x00110008 00000000
```

IRP のメジャーおよびマイナーのコードのテキストに、Windows 10 以降が表示されます、たとえば、"IRP\_MJ\_ファイル\_システム\_コントロール"コード値は、この例の"(d)"では、16 進数も表示されます。

表示出力では、3 番目の引数は、IOCTL コードです。 使用して、 [ **! ioctldecode** ](-ioctldecode.md) IOCTL に関する情報を表示するコマンド。

Windows Vista からこの拡張機能からの出力の例を次に示します。

```dbgcmd
0: kd> !irp 0x831f4a00
Irp is active with 8 stacks 5 is current (= 0x831f4b00)
 Mdl = 82b020d8 Thread 8c622118:  Irp stack trace.
     cmd  flg cl Device   File     Completion-Context
 [  0, 0]   0  0 00000000 00000000 00000000-00000000

                        Args: 00000000 00000000 00000000 00000000
 [  0, 0]   0  0 00000000 00000000 00000000-00000000

                        Args: 00000000 00000000 00000000 00000000
 [  0, 0]   0  0 00000000 00000000 00000000-00000000

                        Args: 00000000 00000000 00000000 00000000
 [  0, 0]   0  0 00000000 00000000 00000000-00000000

                        Args: 00000000 00000000 00000000 00000000
>[  3,34]  40 e1 828517a8 00000000 842511e0-00000000 Success Error Cancel pending
               \Driver\disk     partmgr!PmReadWriteCompletion
 Args: 00007000 00000000 fe084e00 00000004
 [  3, 0]  40 e0 82851450 00000000 842414d4-82956350 Success Error Cancel
 \Driver\PartMgr  volmgr!VmpReadWriteCompletionRoutine
                        Args: 129131bb 000000de fe084e00 00000004
 [  3, 0]   0 e0 82956298 00000000 847eeed0-829e2ba8 Success Error Cancel
 \Driver\volmgr   Ntfs!NtfsMasterIrpSyncCompletionRoutine
                        Args: 00007000 00000000 1bdae400 00000000
 [  3, 0]   0  0 82ac2020 8e879410 00000000-00000000
               \FileSystem\Ntfs
                        Args: 00007000 00000000 00018400 00000000
```

ドライバー名の横にある完了ルーチンは、そのスタックの場所に設定し、下の行で、ドライバーによって設定されていることに注意してください。 前の例では、 **Ntfs! NtfsMasterIrpSyncCompletionRoutine**によって設定された **\\FileSystem\\Ntfs**します。 **完了コンテキスト**上記のエントリ**Ntfs! NtfsMasterIrpSyncCompletionRoutine**、 **847eeed0 829e2ba8**も完了ルーチンのアドレスを示します渡されるコンテキストとして**Ntfs! NtfsMasterIrpSyncCompletionRoutine**します。 このことを確認できますのアドレス**Ntfs! NtfsMasterIrpSyncCompletionRoutine**は**847eeed0**が呼び出されると、このルーチンに渡されるコンテキストと**829e2ba8**.

**IRP の主な機能コード**

次の情報は、この拡張機能コマンドの出力を解釈するのに役立つに含まれています。

IRP の主要な関数のコードは次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主要な関数のコード</th>
<th align="left">16 進コード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MJ_CREATE</p></td>
<td align="left"><p>0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_CREATE_NAMED_PIPE</p></td>
<td align="left"><p>0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_CLOSE</p></td>
<td align="left"><p>0x02</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_READ</p></td>
<td align="left"><p>0x03</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_WRITE</p></td>
<td align="left"><p>0x04</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_QUERY_INFORMATION</p></td>
<td align="left"><p>0x05</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_SET_INFORMATION</p></td>
<td align="left"><p>0x06</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_QUERY_EA</p></td>
<td align="left"><p>0x07</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_SET_EA</p></td>
<td align="left"><p>0x08</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_FLUSH_BUFFERS</p></td>
<td align="left"><p>0x09</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_QUERY_VOLUME_INFORMATION</p></td>
<td align="left"><p>0x0A</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_SET_VOLUME_INFORMATION</p></td>
<td align="left"><p>0x0B</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_DIRECTORY_CONTROL</p></td>
<td align="left"><p>0x0C</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_FILE_SYSTEM_CONTROL</p></td>
<td align="left"><p>0x0D</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_DEVICE_CONTROL</p></td>
<td align="left"><p>0x0E</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
IRP_MJ_INTERNAL_DEVICE_CONTROL IRP_MJ_SCSI</td>
<td align="left"><p>0x0F</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_SHUTDOWN</p></td>
<td align="left"><p>0x10</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_LOCK_CONTROL</p></td>
<td align="left"><p>0x11</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_CLEANUP</p></td>
<td align="left"><p>0x12</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_CREATE_MAILSLOT</p></td>
<td align="left"><p>0x13</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_QUERY_SECURITY</p></td>
<td align="left"><p>0x14</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_SET_SECURITY</p></td>
<td align="left"><p>0x15</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_POWER</p></td>
<td align="left"><p>0x16</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_SYSTEM_CONTROL</p></td>
<td align="left"><p>0x17</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_DEVICE_CHANGE</p></td>
<td align="left"><p>0x18</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MJ_QUERY_QUOTA</p></td>
<td align="left"><p>0x19</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MJ_SET_QUOTA</p></td>
<td align="left"><p>0x1A</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
IRP_MJ_PNP IRP_MJ_MAXIMUM_FUNCTION</td>
<td align="left"><p>0x1B</p></td>
</tr>
</tbody>
</table>

 

プラグ アンド プレイ マイナー関数のコードは次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マイナー関数のコード</th>
<th align="left">16 進コード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_START_DEVICE</p></td>
<td align="left"><p>0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_REMOVE_DEVICE</p></td>
<td align="left"><p>0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_REMOVE_DEVICE</p></td>
<td align="left"><p>0x02</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_CANCEL_REMOVE_DEVICE</p></td>
<td align="left"><p>0x03</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_STOP_DEVICE</p></td>
<td align="left"><p>0x04</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_STOP_DEVICE</p></td>
<td align="left"><p>0x05</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_CANCEL_STOP_DEVICE</p></td>
<td align="left"><p>0x06</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_DEVICE_RELATIONS</p></td>
<td align="left"><p>0x07</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_INTERFACE</p></td>
<td align="left"><p>0x08</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_CAPABILITIES</p></td>
<td align="left"><p>0x09</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_RESOURCES</p></td>
<td align="left"><p>0x0A</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_RESOURCE_REQUIREMENTS</p></td>
<td align="left"><p>0x0B</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_DEVICE_TEXT</p></td>
<td align="left"><p>0x0C</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_FILTER_RESOURCE_REQUIREMENTS</p></td>
<td align="left"><p>0x0D</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_READ_CONFIG</p></td>
<td align="left"><p>0x0F</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_WRITE_CONFIG</p></td>
<td align="left"><p>0x10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_EJECT</p></td>
<td align="left"><p>0x11</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_SET_LOCK</p></td>
<td align="left"><p>0x12</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_ID</p></td>
<td align="left"><p>0x13</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_PNP_DEVICE_STATE</p></td>
<td align="left"><p>0x14</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_BUS_INFORMATION</p></td>
<td align="left"><p>0x15</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_DEVICE_USAGE_NOTIFICATION</p></td>
<td align="left"><p>0x16</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_SURPRISE_REMOVAL</p></td>
<td align="left"><p>0x17</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_LEGACY_BUS_INFORMATION</p></td>
<td align="left"><p>0x18</p></td>
</tr>
</tbody>
</table>

 

WMI のマイナー関数コードは次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マイナー関数のコード</th>
<th align="left">16 進コード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_QUERY_ALL_DATA</p></td>
<td align="left"><p>0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_SINGLE_INSTANCE</p></td>
<td align="left"><p>0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_CHANGE_SINGLE_INSTANCE</p></td>
<td align="left"><p>0x02</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_CHANGE_SINGLE_ITEM</p></td>
<td align="left"><p>0x03</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_ENABLE_EVENTS</p></td>
<td align="left"><p>0x04</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_DISABLE_EVENTS</p></td>
<td align="left"><p>0x05</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_ENABLE_COLLECTION</p></td>
<td align="left"><p>0x06</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_DISABLE_COLLECTION</p></td>
<td align="left"><p>0x07</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_REGINFO</p></td>
<td align="left"><p>0x08</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_EXECUTE_METHOD</p></td>
<td align="left"><p>0x09</p></td>
</tr>
</tbody>
</table>

 

電源管理のマイナー関数コードは次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マイナー関数のコード</th>
<th align="left">16 進コード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_WAIT_WAKE</p></td>
<td align="left"><p>0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_POWER_SEQUENCE</p></td>
<td align="left"><p>0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_SET_POWER</p></td>
<td align="left"><p>0x02</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_QUERY_POWER</p></td>
<td align="left"><p>0x03</p></td>
</tr>
</tbody>
</table>

 

SCSI マイナー関数のコードは次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マイナー関数のコード</th>
<th align="left">16 進コード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_SCSI_CLASS</p></td>
<td align="left"><p>0x01</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**! irpfind**](-irpfind.md)

[**! ioctldecode**](-ioctldecode.md)

 

 






