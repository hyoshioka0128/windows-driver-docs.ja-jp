---
title: Windows Vista のオーディオ エンジンの調査
description: Windows Vista のオーディオ エンジンの調査
ms.assetid: 6301f6d7-57f5-4b9f-9567-57efb9dc58f3
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: b7dd26437fba19251729fe31dc9a8b92a4564465
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558630"
---
# <a name="exploring-the-windows-vista-audio-engine"></a>Windows Vista のオーディオ エンジンの調査


このトピックでは、Windows Vista のオーディオ エンジンの概要を示します。 APOs と sAPOs 連携させる方法を理解するのに役立つ概念に焦点を当てます。

次の図は、オーディオ エンジンの内部構造の簡略化されたレイアウトを表示します。

![簡略化されたレイアウトをエンジンの windows vista のオーディオを示す図](images/sysfxapo-custom-details.png)

図として表示されます、システム提供 APOs および sAPOs はオーディオ エンジンの基本的な構成要素です。 オーディオ エンジンは、パイプと呼ばれるコンポーネントをシステム提供の APOs と sAPOs を構成します。 オーディオ エンジンでパイプの 2 種類あります。

-   Stream パイプは APOs と sAPOs ストリームに単一のアプリケーションから、ローカルではデジタル オーディオ処理を実行するのに構成されます。 この種類のパイプ sAPO はローカル効果 sAPO (LFX sAPO) と呼ばれます。

-   デバイスのパイプは APOs と sAPOs すべてのストリームをグローバルに影響を与えるデジタル オーディオ処理を実行するのに構成されます。 この種類のパイプ sAPO はグローバル効果 sAPO (GFX sAPO) と呼ばれます。

次の表では、Windows Vista のオーディオ エンジンと、それらが適用されるシステム エフェクトの種類で利用できる sAPOs を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows Vista sAPO</th>
<th align="left">システムの効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>低音ブーストします。</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>低音の管理</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ラウドネス イコライゼーション</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>低頻度の保護</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>スピーカー フィル</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>スピーカーのファントム</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>仮想サラウンド</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッドホンで仮想化されたブロックの挿入</p></td>
<td align="left"><p>LFX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ポータブル コンピューターのサウンドを強化</p></td>
<td align="left"><p>GFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>ルーム コレクション</p></td>
<td align="left"><p>GFX</p></td>
</tr>
</tbody>
</table>

 

オーディオのアプリケーションでは、オーディオ処理を開始するときに、オーディオ エンジンは、デジタル オーディオ データを処理するオーディオのグラフにシステム提供しないと、sAPOs を構成します。 オーディオ エンジンがオーディオのグラフを構築するために使用するメカニズムは、システムの詳細では説明しません。

オーディオのアプリケーションには、共有モードまたは排他モードで接続を開始できます。 SAPOs の既定のセットは、Windows Vista にインストールされますが、sAPOs システム コンポーネントであると見なされない、したがってカスタマイズが可能です。

### <a name="span-idsharedmodespanspan-idsharedmodespanshared-mode"></a><span id="shared_mode"></span><span id="SHARED_MODE"></span>共有モード

共有モードでは、オーディオのアプリケーションは、他のオーディオのアプリケーションの他のプロセスで実行されているオーディオ ハードウェアを共有します。 オーディオ エンジンでは、これらのアプリケーションからのストリームが混在し、ハードウェアを結果として得られるミックスを再生します。 共有モードでストリームを表示する任意のアプリケーションでは、オーディオ エンジンによって使用される形式をミックスを選択する必要があります。 共有モードを使用する利点は、Windows Vista のオーディオ エンジンが、組み込みオーディオ処理オブジェクト (APO) ために必要なサポート機能を提供するを提供します。 共有モードを使用することの欠点は、オーディオ ストリームの待機時間が排他モードでは、それよりも多いことです。 次のコード例では、共有モードでのオーディオ ストリームを初期化するための構文を示します。

```cpp
 hResult = pAudioClient->Initialize(
        AUDCLNT_SHAREMODE_SHARED, 
        0,
        0,
        0,
 pWfx,
        &m_SubmixGuid);
```

### <a name="span-idexclusivemodespanspan-idexclusivemodespanexclusive-mode"></a><span id="exclusive_mode"></span><span id="EXCLUSIVE_MODE"></span>排他モード

これに対し、排他モードでアプリケーションがストリームを開くと、ときに、アプリケーションには、オーディオ ハードウェアへの排他アクセスがあります。 このモードでは、アプリケーションは、エンドポイントをサポートする任意のオーディオ形式を選択できます。 排他モードを使用する利点は、オーディオ ストリームの待機時間が共有モードではよりも低くします。 排他モードを使用しての欠点は、処理、オーディオ エンジンの機能をサポートするために、独自の APO を指定する必要があります。 プロフェッショナル レベルのアプリケーションの数が少ないだけでは、この操作モードが必要です。 次のコード例では、排他モードでのオーディオ ストリームを初期化するための構文を示します。

```cpp
 hResult = pAudioClient->Initialize(
            AUDCLNT_SHAREMODE_EXCLUSIVE,
            0,
            0,
            0,  
 pWfxEx,
            &m_SubmixGuid);
```

アプリケーションは、オーディオ処理を開始すた後、グラフ ビルダーは、オーディオのグラフに、sAPOs を構成し、sAPOs 初期化もします。 オーディオのサービスは、sAPO の入出力にオーディオ データ形式を確立するために LFX sAPO とネゴシエートします。 詳細については、次を参照してください。[形式ネゴシエーション](format-negotiation.md)します。

 

 




