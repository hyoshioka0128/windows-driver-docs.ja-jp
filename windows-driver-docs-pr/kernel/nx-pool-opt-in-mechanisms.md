---
title: NX プールのオプトインメカニズム
description: 以前のバージョンの Windows から Windows 8 にカーネルモードドライバーコードを移植するには、ベストプラクティスとして NonPagedPoolNx 型のメモリプールを使用する必要があります。
ms.assetid: 9C868569-14EC-4915-8553-FD2D94C5A855
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4e16323cb67bd2fe58d7c051e9dd1080ad1ab9f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838534"
---
# <a name="nx-pool-opt-in-mechanisms"></a>NX プールのオプトインメカニズム


以前のバージョンの Windows から Windows 8 にカーネルモードドライバーコードを移植するには、ベストプラクティスとして**NonPagedPoolNx**型のメモリプールを使用する必要があります。 いくつかの移植補助機能のいずれかを使用して、既定で**NonPagedPoolNx**プールの種類を使用することを簡単に選択できます。

これらの移植支援では、次のいずれかまたは両方の方法を使用して、ドライバーが NX 非ページプールを使用できるようにします。

-   `#define` プリプロセッサステートメントを使用して、グローバルに定義されたマクロ名を作成します。

-   [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンからインライン関数を呼び出します。

ほとんどのカーネルモードドライバーコードでは、これらの移植機能により、開発者は最小限の労力でドライバーを更新できます。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="single-binary-opt-in-pool-nx-optin.md" data-raw-source="[Single Binary Opt-In: POOL_NX_OPTIN](single-binary-opt-in-pool-nx-optin.md)">シングルバイナリオプトイン: POOL_NX_OPTIN</a></p></td>
<td><p>Windows 8 と以前のバージョンの Windows の両方で実行される単一のドライバーバイナリをビルドするには、POOL_NX_OPTIN オプトイン機構を使用します。 これは、複数の Windows バージョンをサポートするために1つのドライバーバイナリを提供するサードパーティ製ハードウェアベンダー向けの移植支援です。</p></td>
</tr>
<tr class="even">
<td><p><a href="multiple-binary-opt-in-pool-nx-optin-auto.md" data-raw-source="[Multiple Binary Opt-In: POOL_NX_OPTIN_AUTO](multiple-binary-opt-in-pool-nx-optin-auto.md)">複数のバイナリオプトイン: POOL_NX_OPTIN_AUTO</a></p></td>
<td><p>異なるバージョンの Windows に対して異なるドライバーバイナリを提供するハードウェアベンダーの場合は、POOL_NX_OPTIN_AUTO オプトインメカニズムを使用できます。 この移植支援は、Windows 8 用の個別のドライバーバイナリと、ドライバーでサポートされている以前のバージョンの Windows のそれぞれをビルドします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="selective-opt-out-pool-nx-optout.md" data-raw-source="[Selective Opt-Out: POOL_NX_OPTOUT](selective-opt-out-pool-nx-optout.md)">選択的オプトアウト: POOL_NX_OPTOUT</a></p></td>
<td><p>一連のドライバーソースファイルに対して、実行されていない (NX) プールオプトイン機構のいずれかをグローバルに有効にしてから、POOL_NX_OPTOUT で選択した1つ以上のソースファイルに対してこのオプトイン機構をオーバーライドできます。 これにより、選択したソースファイルは、実行可能な非ページメモリを引き続き使用できます。 POOL_NX_OPTOUT オプトアウト機構は、POOL_NX_OPTIN または POOL_NX_OPTIN_AUTO のいずれかのオプトインメカニズムで使用できます。</p></td>
</tr>
</tbody>
</table>

 

 

 




