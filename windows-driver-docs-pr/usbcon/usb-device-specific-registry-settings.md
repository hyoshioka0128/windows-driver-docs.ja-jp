---
Description: This topic describes the device-specific registry entries.
title: USB デバイスのレジストリ エントリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b8308e45f36a8261a2787ebbfed7160745f2e3a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559102"
---
# <a name="usb-device-registry-entries"></a>USB デバイスのレジストリ エントリ


このトピックでは、デバイス固有のレジストリ エントリを説明します。

## <a name="find-device-information-after-it-enumerates-on-windows"></a>Windows 上に列挙した後、デバイス情報を検索します。


**デバイスのインターフェイス、デバイスの GUID、ハードウェア Id、およびデバイスのクラス情報を表示します。**

1.  このレジストリ キーとメモを見つけ、 **DeviceInstance**値。

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\DeviceClasses\\**

    ![usb ハードウェア id](images/deviceinstance.png)

2.  デバイス インスタンスのレジストリ キーを検索して、デバイス インターフェイスの GUID を取得します。

    **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\Enum\\USB\\&lt;ハードウェア id&gt; \\ &lt;インスタンス id&gt;\\デバイス パラメーター**

    ![usb デバイス インターフェイスの guid](images/device-interface-guid2.png)

3.  デバイス インスタンス キーの下のデバイス クラスやサブクラスでは、プロトコルのコードに注意してください。

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\USB**

    ![usb デバイス クラスのサブクラス プロトコル コード](images/deviceclass.png)

## <a name="registry-settings-for-configuring-usb-driver-stack-behavior"></a>USB ドライバー スタックの動作を構成するためのレジストリ設定


このトピックで説明されているレジストリ エントリはこのキーの下にあります。

```cpp
HKEY_LOCAL_MACHINE
   SYSTEM
      CurrentControlSet
         Control
            usbflags
               <VVVVPPPPRRRR>
                  <Device-specific registry entry>
```

***Vvvvpppprrrrr***キー

-   *vvvv*ベンダーを識別する 4 桁の 16 進数には
-   *pppp* 4 桁の 16 進数、製品を識別するには
-   *rrrr*はデバイスのリビジョン番号が含まれる 4 桁の 16 進数。

ベンダー ID、製品 ID、およびリビジョン番号の値がから取得した、 [USB デバイス記述子](usb-device-descriptors.md)します。
次の表のレジストリ エントリ、 ***vvvvpppprrrrr***キー。 USB ドライバー スタックは、読み取り専用の値としてこれらのエントリを考慮します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>レジストリ エントリ</th>
<th>説明</th>
<th>設定可能な値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>osvc</strong></p>
<p>REG_BINARY</p>
<p>Windows XP 以降のバージョンでサポートされます。</p></td>
<td><p>オペレーティング システムでのデバイスを照会するかどうかを示します<a href="microsoft-defined-usb-descriptors.md" data-raw-source="[Microsoft-Defined USB Descriptors](microsoft-defined-usb-descriptors.md)">Microsoft-Defined の USB ディスクリプター</a>します。 OS 記述子の前に試行したクエリが成功した場合、値には、OS の文字列記述子から仕入先のコードが含まれています。</p></td>
<td><ul>
<li><p>0x0000:デバイスは、Microsoft OS 文字列記述子の要求に有効な応答を提供しませんでした。</p></li>
<li><p>0x01xx:デバイスには、xx は、Microsoft OS 文字列記述子の要求に有効な応答が提供されている、 <strong>bVendorCode</strong>応答に含まれています。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>IgnoreHWSerNum</strong></p>
<p>REG_BINARY</p>
<p>Windows Vista 以降のバージョンでサポートされます。</p></td>
<td><p>USB ドライバー スタックが、デバイスのシリアル番号を無視する必要があるかどうかを示します。</p></td>
<td><ul>
<li><p>0x0000:設定を無効になります。</p></li>
<li><p>0x0001:デバイスのシリアル番号を無視する USB ドライバー スタックを強制します。 デバイス インスタンスでは、デバイスが接続されているポートに関連付けられています。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>ResetOnResume</strong></p>
<p>REG_BINARY</p>
<p>Windows Vista 以降のバージョンでサポートされます。</p></td>
<td><p>ポートが、サイクルをスリープから再開するときに、USB ドライバー スタックがデバイスをリセットする必要があるかどうかを示します。</p></td>
<td><ul>
<li><p>0x0000:設定を無効になります。</p></li>
<li><p>0x0001:強制的にポート上のデバイスをリセットする USB ドライバー スタックを再開します。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



