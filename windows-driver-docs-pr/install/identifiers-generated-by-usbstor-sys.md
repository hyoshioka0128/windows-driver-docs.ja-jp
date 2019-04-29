---
title: USBSTOR.SYS によって生成された識別子
description: USBSTOR.SYS によって生成された識別子
ms.assetid: 5a5e1b68-9ec7-4a74-9b21-25f158a2a46c
keywords:
- USBSTOR します。SYS WDK デバイスのインストール
- デバイス Id の WDK デバイスのインストール
- USB 記憶装置ポート ドライバー WDK デバイスのインストール
- 記憶域ポート ドライバー WDK デバイスのインストール
- ハードウェア Id の WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50bed89d8b75bd90087c5a4a129570bed30ea29f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327814"
---
# <a name="identifiers-generated-by-usbstorsys"></a>USBSTOR.SYS によって生成された識別子





Windows 2000 以降、オペレーティング システムは、多くの USB 大容量記憶装置デバイスのネイティブ サポートを提供します。 *Usbstor.inf*インストール ファイルに明示的にサポートされているデバイスのデバイス Id が含まれています。 USB ハブのドライバーでは、これらのデバイスを列挙する場合、オペレーティング システムが自動的に、USB ストレージ ポート ドライバーを読み込む*Usbstor.sys*します。

Usb デバイス Id で記憶装置の質量*Usbstor.inf* USB デバイスの Id が、USB デバイスのデバイスの記述子の情報を使用して構成の通常の形式になります。

USB\\VID_v(4) & PID_d(4) REV_r(4)

各項目の意味は次のとおりです。

-   *v(4)* 仕入先に、USB 委員会を代入する 4 桁の仕入先のコードに示します。

-   *d(4)* 4 桁のプロダクト コードは、ベンダーがデバイスに割り当てます。

-   *r(4)* リビジョン コードに示します。

これらのデバイス Id だけでなく*Usbstor.inf*クラス 8 ATAPI CD-ROM とリムーバブル メディア デバイス一括のみの転送をサポートする互換性 Id が含まれています。

USB\\CLASS_08 &AMP; SUBCLASS_02 PROT_50

USB\\CLASS_08 &AMP; SUBCLASS_05 PROT_50

USB\\CLASS_08 &AMP; SUBCLASS_06 PROT_50

各項目の意味は次のとおりです。

-   08 h をクラスの大容量記憶装置を = です。

-   サブクラス 02 h = SFF 8020i ATAPI CD-ROM デバイス。

-   サブクラス 05 h SFF 8070i ATAPI リムーバブル メディアを = です。

-   サブクラス 06 h 汎用 SCSI メディアを = です。

-   プロトコルの 50 h = 一括専用のトランスポート プロトコル。

オペレーティング システムが負荷になっている場合は、デバイスのデバイスの記述子から取得されたデータでは、これらの互換性のある id と一致する、 *Usbstor.sys*します。

読み込まれるとすぐに、USB 記憶域のポート ドライバーは、各デバイスの論理ユニットを新しい PDO を作成します。 詳細については、によって作成されたデバイス スタックの例を参照してください。 *Usbstor.sys*に[USB 大容量記憶装置のデバイス オブジェクトの例](https://msdn.microsoft.com/windows/hardware/drivers/storage/device-object-example-for-a-usb-mass-storage-device)します。

PnP マネージャー クエリを新しく作成された Pdo の識別文字列についてには、USB 記憶域ポート ドライバーでは、デバイスの新しいセットを作成するとき、デバイスの SCSI 問い合わせデータからハードウェアおよび互換性 Id が派生します。 デバイス ID の形式は次のとおりです。

USBSTOR\\v(8)p(16)r(4)

各項目の意味は次のとおりです。

-   *v(8)* 8 文字の仕入先識別子です。

-   *p(16)* は 16 文字のプロダクトの識別子です。

-   *r(4)* は 4 文字のリビジョン レベル値です。

ディスク ドライブのデバイス ID の例に次のようになります。

USBSTOR\\SEAGATE_ST39102LW___0004

ハードウェア、USB ストレージ ポート ドライバーによって生成される Id がような。

USBSTOR\\t\*v(8)p(16)r(4)

USBSTOR\\t\*v(8)p(16)

USBSTOR\\t\*v(8)

USBSTOR\\v(8)p(16)r(1)

v(8)p(16)r(1)

USBSTOR\\GenericTypeString

GenericTypeString

各項目の意味は次のとおりです。

- *t\** は可変長の SCSI デバイス種類コード。

- *v(8)* 8 文字の仕入先識別子です。

- *p(16)* は 16 文字のプロダクトの識別子です。

- *r(4)* は 4 文字のリビジョン レベル値です。 これらの他の識別子で*r(1)* リビジョン識別子の最初の文字だけを表します。

次の表には、識別子文字列を生成する USB 記憶域ポート ドライバーで使用する SCSI デバイスの種類のコードが含まれています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SCSI 型コード</th>
<th align="left">デバイスの種類</th>
<th align="left">ジェネリック型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DIRECT_ACCESS_DEVICE (0)</p></td>
<td align="left"><p>ディスクまたは SFloppy</p></td>
<td align="left"><p>GenDisk または GenSFloppy</p></td>
</tr>
<tr class="even">
<td align="left"><p>SEQUENTIAL_ACCESS_DEVICE (1)</p></td>
<td align="left"><p>シーケンシャル</p></td>
<td align="left"><p>GenSequential</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WRITE_ONCE_READ_MULTIPLE_DEVICE (4)</p></td>
<td align="left"><p>ワーム</p></td>
<td align="left"><p>GenWorm</p></td>
</tr>
<tr class="even">
<td align="left"><p>READ_ONLY_DIRECT_ACCESS_DEVICE (5)</p></td>
<td align="left"><p>CdRom</p></td>
<td align="left"><p>GenCdRom</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OPTICAL_DEVICE (7)</p></td>
<td align="left"><p>光学式</p></td>
<td align="left"><p>GenOptical</p></td>
</tr>
<tr class="even">
<td align="left"><p>MEDIUM_CHANGER (8)</p></td>
<td align="left"><p>チェンジャー</p></td>
<td align="left"><p>GenChanger</p></td>
</tr>
<tr class="odd">
<td align="left"><p>既定の種類 (前述のないすべての値)</p></td>
<td align="left"><p>その他</p></td>
<td align="left"><p>UsbstorOther</p></td>
</tr>
</tbody>
</table>

 

これらの例では、ハードウェア、USB ストレージ ポート ドライバーによって生成される Id を示します。

USBSTOR\\DiskSEAGATE_ST39102LW___0004

USBSTOR\\DiskSEAGATE_ST39102LW___

USBSTOR\\DiskSEAGATE_

USBSTOR\\SEAGATE_ST39102LW___0

SEAGATE_ST39102LW_______0

USBSTOR\\GenDisk

GenDisk

USB 記憶域ポート ドライバーでは、2 つの互換性のある Id を生成します。

USBSTOR\\t\*

USBSTOR\\RAW

場所*t\** は可変長の SCSI デバイス種類コード。

USB 記憶域ポート ドライバーによって生成された互換性 Id は次の例に示します。

USBSTOR\\ディスク

USBSTOR\\RAW

 

 





