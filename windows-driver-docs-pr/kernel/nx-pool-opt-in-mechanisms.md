---
title: NX プールのオプトイン メカニズム
description: 以前のバージョンの Windows、Windows 8 にポート カーネル モード ドライバー コードにベスト プラクティスとして、メモリ プールの NonPagedPoolNx 型を使用する必要があります。
ms.assetid: 9C868569-14EC-4915-8553-FD2D94C5A855
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9c8426d553eed9624d1fd2027dd04b21d6f685dc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365416"
---
# <a name="nx-pool-opt-in-mechanisms"></a>NX プールのオプトイン メカニズム


以前のバージョンの Windows、Windows 8 にポート カーネル モード ドライバー コードに使用する必要があります、 **NonPagedPoolNx**ベスト プラクティスとして、メモリ プールの種類。 移植ツールがいくつかのいずれかを使用して、簡単に「オプトイン」を使用することができます、 **NonPagedPoolNx**既定プールの種類。

NX を使用するドライバーを有効にする、次の手法の一方または両方を使用して移植補助これら非ページ プール。

-   使用して、`#define`プリプロセッサ ステートメントをグローバルに定義されたマクロ名を作成します。

-   インライン関数を呼び出し、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。

ほとんどのカーネル モード ドライバーのコードでは、これらへの移植の補助には、開発者は最小限の労力で、ドライバーの更新が有効にします。

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
<td><p><a href="single-binary-opt-in-pool-nx-optin.md" data-raw-source="[Single Binary Opt-In: POOL_NX_OPTIN](single-binary-opt-in-pool-nx-optin.md)">単一バイナリにオプトインします。POOL_NX_OPTIN</a></p></td>
<td><p>Windows 8 と Windows の以前のバージョンの両方を実行している 1 つのドライバー バイナリをビルドするには、POOL_NX_OPTIN オプトイン メカニズムを使用します。 これは、複数の Windows バージョンをサポートするためにバイナリの 1 つのドライバーを提供するサード パーティ製ハードウェア ベンダーの移植の支援です。</p></td>
</tr>
<tr class="even">
<td><p><a href="multiple-binary-opt-in-pool-nx-optin-auto.md" data-raw-source="[Multiple Binary Opt-In: POOL_NX_OPTIN_AUTO](multiple-binary-opt-in-pool-nx-optin-auto.md)">複数バイナリ オプトインします。POOL_NX_OPTIN_AUTO</a></p></td>
<td><p>ハードウェア ベンダーが Windows のバージョンごとに別のドライバー バイナリを提供している場合は、POOL_NX_OPTIN_AUTO オプトイン メカニズムを使用することができます。 この移植の補助は、Windows 8 以降、ドライバーがサポートする Windows の以前のバージョンごとに個別のドライバー バイナリをビルドします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="selective-opt-out-pool-nx-optout.md" data-raw-source="[Selective Opt-Out: POOL_NX_OPTOUT](selective-opt-out-pool-nx-optout.md)">選択的オプトアウトします。POOL_NX_OPTOUT</a></p></td>
<td><p>メカニズム一連のドライバーのソース ファイルのオプトイン プールのデータ実行 (NX) のいずれかをグローバルに有効にして、POOL_NX_OPTOUT で 1 つまたは複数の選択したソース ファイルをこのオプトイン メカニズムをオーバーライドすることができます。 これにより、実行可能ファイルの非ページ メモリの使用継続を選択したソース ファイルができます。 POOL_NX_OPTIN または POOL_NX_OPTIN_AUTO オプトイン メカニズムのいずれかで POOL_NX_OPTOUT のオプトアウト メカニズムを使用することができます。</p></td>
</tr>
</tbody>
</table>

 

 

 




