---
title: RPC 状態情報を有効にする
description: RPC 状態情報を有効にする
ms.assetid: 8804d941-c241-44cb-8d91-05b94a875d94
keywords:
- RPC デバッグ、RPC 状態情報を有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6c3a5a9b29664527dec139283d56ef2ba31020d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572563"
---
# <a name="enabling-rpc-state-information"></a>RPC 状態情報を有効にする


## <span id="ddk_enabling_rpc_state_information_dbg"></span><span id="DDK_ENABLING_RPC_STATE_INFORMATION_DBG"></span>


2 つの異なるレベルの RPC ランタイム状態情報を収集できます。**Server**情報と**完全**情報。 デバッガーの前に、この情報の収集を有効にする必要があります。 またはさせるためは、状態情報を分析するために使用できます。

Windows XP と Windows の以降のバージョンのみ、RPC 状態情報の収集をサポートします。

収集**Server**状態情報は非常に軽量です。 パフォーマンス テスト中にあっても検出可能な負荷がまったくない、その結果、RPC 呼び出しの約 100 個のマシン語命令のコストがかかります。 この情報を収集してメモリ (約 4 KB RPC サーバーあたり) を使用して、メモリ不足が既に発生しているコンピューターではお勧めできません。 **Server**情報には、エンドポイント、スレッド、接続オブジェクト、およびサーバーを呼び出す (SCALL) のオブジェクトに関するデータが含まれています。 これは、ほとんどの RPC の問題をデバッグするための十分です。

収集**完全**状態情報は、複数の重量。 収集されたすべての情報が含まれています、 **Server**レベルと、さらに、クライアントの呼び出し (CCALL) オブジェクトが含まれています。 **完全な**状態情報は通常必要ありません。

個々 のコンピューターで収集するには、状態情報を有効にするには、グループ ポリシー エディター (Gpedit.msc) を実行します。 ローカル コンピューター ポリシー の下に移動します。**コンピューター構成/管理用テンプレート/システム/リモート プロシージャ コール**します。 このノードが表示されます、 **RPC トラブルシューティング状態情報**項目。 そのプロパティを編集するときに、5 つの可能な状態が表示されます。

<span id="None"></span><span id="none"></span><span id="NONE"></span>**[なし]**  
状態情報は維持されません。 コンピューターでメモリ不足が発生している場合を除き、これは推奨されません。

<span id="Server"></span><span id="server"></span><span id="SERVER"></span>**サーバー**  
**Server**状態情報が収集されます。 これは、1 台のコンピューター上の推奨設定です。

<span id="Full"></span><span id="full"></span><span id="FULL"></span>**完全です**  
**完全な**状態情報が収集されます。

<span id="Auto1"></span><span id="auto1"></span><span id="AUTO1"></span>**Auto1**  
同じ 64 MB 未満の RAM でコンピューターがこの**None**します。 少なくとも 64 MB の RAM でコンピューターは、これと同じ**Server**します。

<span id="Auto2"></span><span id="auto2"></span><span id="AUTO2"></span>**Auto2**  
これと同じである 128 MB の RAM、未満を使用して Windows Server 2003 を実行しているコンピューターまたは Windows XP コンピューターでは、 **None**します。 同じで、少なくとも 128 MB の RAM での Windows Server 2003 コンピューターではこの**Server**します。

既定値です。

同時に、一連のネットワークに接続されたコンピューターでこれらのレベルを設定する場合は、マシンの推奨セットをコンピューターのポリシーをロールアウトするグループ ポリシー エディターを使用します。 ポリシー エンジンにより自動的に希望の設定は、マシンの推奨セットに反映されます。 **Auto1**と**Auto2**レベルは特にそれがここでは、オペレーティング システムと各コンピューターの RAM の量が異なるためです。

ネットワークには、Windows は Windows XP よりも前のバージョンを実行しているコンピューターが含まれている場合は、これらのコンピューターで、設定が無視されます。

 

 





