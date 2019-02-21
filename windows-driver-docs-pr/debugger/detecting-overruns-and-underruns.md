---
title: アンダーラン オーバーランを検出
description: アンダーラン オーバーランを検出
ms.assetid: d7d282c8-adde-49fc-a20e-d633abd6dd3f
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14eed792f1d8c57a75d125d84fbffb4e2ddd025d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538509"
---
# <a name="detecting-overruns-and-underruns"></a>アンダーラン オーバーランを検出


## <span id="ddk_detecting_overruns_and_underruns_dtools"></span><span id="DDK_DETECTING_OVERRUNS_AND_UNDERRUNS_DTOOLS"></span>


使用することができます、**確認を開始**または**終了の確認**GFlags ベストように特別なプールから割り当てを配置するオプションが (メモリ割り当ての末尾へのアクセス) オーバーランの検出に最適なまたはアンダーラン (割り当ての先頭の前にメモリにアクセスする)。

-   **開始の確認**有効アンダーラン特別なプールから割り当てを検出します。 これにより、プログラムが前に特別なプールのメモリの割り当てメモリへのアクセスを試みると、バグ チェック。

-   **終了の確認**特別なプールから割り当てで検出をオーバーランできるようにします。 バグ チェックは、プログラムは特別なプールのメモリの割り当てを超えるメモリにアクセスしようとしました。 これにより、します。 オーバーランははるかに一般的なは、**終了の確認**既定値です。

Windows Vista および以降のバージョンの Windows では、このオプションで使用できる、**システム レジストリ**と**カーネル フラグ**タブ。 Windows の以前のバージョンでのみ使用できますが、**システム レジストリ**タブ。

**特別なプールの配置を指定するには**

1.  をクリックして、**システム レジストリ**タブ。

2.  をクリックして**開始を確認します。** または**終了を確認します。** します。

3.  **[適用]** をクリックします。

    次のスクリーン ショットは、システムの確認を開始および終了のことを確認の設定を示しています**レジストリ**タブ。

    ![検証方法を示すスクリーン ショットが開始し、システム レジストリ タブで、終了オプションを確認します。](images/gflags-overruns.png)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**開始を確認します**と**終了の確認**配置設定は、特別なプールの割り当て要求の Driver Verifier で設定を含む、特別なプールから、すべての割り当てに適用されます。 配置プールの割り当てまたはタグのサイズを指定せずに設定した場合、ドライバーの検証ツールで設定する要求のみにし、設定が適用されます。

 

 





