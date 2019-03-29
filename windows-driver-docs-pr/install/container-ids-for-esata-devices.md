---
title: eSATA デバイス用のコンテナー ID
description: eSATA デバイス用のコンテナー ID
ms.assetid: 991836f1-936c-4051-ac3b-ad491a4ca221
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaed1ce1561160010eb92b57bc375a277155c142
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581456"
---
# <a name="container-ids-for-esata-devices"></a>eSATA デバイス用のコンテナー ID


外部 Serial Advanced Technology Attachment (eSATA) バスは、コンテナー ID を報告できません。 Windows オペレーティング システム、eSATA デバイスのグループ化デバイス コンテナーと判断した場合は、ATA のバス ドライバーが返すリムーバブル機能に依存します。

ATA のバス ドライバーは、eSATA デバイスは、次の高度なホスト コント ローラー インターフェイス (AHCI) 登録ビットを読み取ることによってリムーバブルを決定します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">AHCI 登録</th>
<th align="left">バイト オフセット</th>
<th align="left">ビットの場所</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HBA の機能 (CAP))</p></td>
<td align="left"><p>0x000</p></td>
<td align="left"><p>5 - 外部 SATA (SXS) をサポートしています。</p></td>
<td align="left"><p>1 に設定すると、このビット値は、ホスト バス アダプター (HBA) が 1 つ以上の SATA ポート (eSATA コネクタの場合) など、外部使用可能である信号専用のコネクタの使用を示します。</p>
<p>ソフトウェアが特定のポートにシグナル専用のコネクタと外部で使用可能なシグナル コネクタがあるかどうかを判断する PxCMD.ESP ビットを参照できますこのビットが 1 に設定されている場合 (つまり、電源はそのコネクタの一部)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>コマンドと状態 (PxCMD) x のポート</p></td>
<td align="left"><p>0x18</p></td>
<td align="left"><p>18 のホット プラグ可能なポート (HPCP)</p></td>
<td align="left"><p>1 に設定すると、このビット値は、ポートのシグナルと電力のコネクタが共同シグナルと電源コネクタを介して外部から利用できることを示します。</p>
<p></p>
<div class="alert">
<strong>注</strong>  これはホット プラグ機能をサポートする blindmate コネクタにのみ適用されます。
</div>
<div>
 
</div>
.</td>
</tr>
<tr class="odd">
<td align="left"><p>コマンドと状態 (PxCMD) x のポート</p></td>
<td align="left"><p>0x18</p></td>
<td align="left"><p>21-外部 SATA ポート (ESP)</p></td>
<td align="left"><p>1 に設定すると、このビット値は、ポートのシグナルのコネクタが信号専用コネクタ (eSATA コネクタの場合) などの外部から利用できることを示します。 このため、ポート ホットプラグ イベントが発生する可能性があります。</p>
<p>ESP が 1 に設定されている場合は、PxCMD.HPCP のビットが 0 と CAP をクリアする必要があります。SXS ビットは、1 に設定する必要があります。</p></td>
</tr>
</tbody>
</table>

 

ATA のバス ドライバーでは、次のいずれかが true の場合、リムーバブルとして eSATA ポートに接続されている任意のデバイスをマークします。

-   HPCP ビットは、eSATA ポートが、ホット プラグ操作をサポートする外部ポートであることを示す 1 に設定されます。

-   SXS と ESP のビットは、どちらも、SATA ポートが、外部の信号専用のポートであることを示す 1 に設定されます。

**注**  これらの条件が相互に排他的です。 外部のホット プラグ-対応ポートまたは外部の信号専用ポート両方ではなく自体のいずれかを指定するには eSATA ポートを宣言できます。

 

SATA、eSATA インターフェイスの詳細についてを参照してください、[シリアル ATA 高度なホスト コント ローラー インターフェイス (AHCI) 1.3 仕様](https://go.microsoft.com/fwlink/p/?linkid=148284)します。

 

 





