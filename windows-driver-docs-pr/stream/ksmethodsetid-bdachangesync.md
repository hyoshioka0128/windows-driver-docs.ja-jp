---
title: KSMETHODSETID\_BdaChangeSync
description: KSMETHODSETID\_BdaChangeSync
ms.assetid: 260b227d-0d49-4efa-8f8c-4c66886cf9f6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 967b6582f0013b47f77b6014b1152ae8137ea8d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530259"
---
# <a name="ksmethodsetidbdachangesync"></a>KSMETHODSETID\_BdaChangeSync


## <span id="ddk_ksmethodsetid_bdachangesync_ks"></span><span id="DDK_KSMETHODSETID_BDACHANGESYNC_KS"></span>


KSMETHODSETID\_BdaChangeSync は BDA 変更の同期メソッドのセット。 フィルター、pin、およびノードのプロパティの要求の一覧を調整するために使用されます。

次の方法を使用できます。

<span id="KSMETHOD_BDA_START_CHANGES"></span><span id="ksmethod_bda_start_changes"></span>[**KSMETHOD\_BDA\_開始\_の変更**](ksmethod-bda-start-changes.md)  
変更リストをリセットし、一連の変更の追跡を開始します。

<span id="KSMETHOD_BDA_CHECK_CHANGES"></span><span id="ksmethod_bda_check_changes"></span>[**KSMETHOD\_BDA\_確認\_の変更**](ksmethod-bda-check-changes.md)  
要求された変更の一覧は動作になっているかどうかを判断します。

<span id="KSMETHOD_BDA_COMMIT_CHANGES"></span><span id="ksmethod_bda_commit_changes"></span>[**KSMETHOD\_BDA\_コミット\_の変更**](ksmethod-bda-commit-changes.md)  
要求された変更の一覧をコミットします。

<span id="KSMETHOD_BDA_GET_CHANGE_STATE"></span><span id="ksmethod_bda_get_change_state"></span>[**KSMETHOD\_BDA\_取得\_変更\_状態**](ksmethod-bda-get-change-state.md)  
フィルターの現在の状態の変更が決定します。

### <a name="comments"></a>コメント

このメソッドのセットは、フィルターに実装されます。 ネットワーク プロバイダーのフィルターは、このメソッドの変更の一覧を開始し、変更を行って、それらを一度にすべてコミットに設定を使用できます。

 

 





