---
title: バグ チェック 0x17E MICROCODE_REVISION_MISMATCH
description: MICROCODE_REVISION_MISMATCH のバグ チェックでは、0x0000017E の値を持ちます。 これは、マルチプロセッサの構成で 1 つまたは複数のプロセッサが一貫性のないマイクロ コードが読み込まれたことを示します。
keywords:
- バグ チェック 0x17E MICROCODE_REVISION_MISMATCH
- MICROCODE_REVISION_MISMATCH
ms.date: 01/14/2019
topic_type:
- apiref
api_name:
- MICROCODE_REVISION_MISMATCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6f125c34cebd91168a97d7fae08f940873efbb17
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519874"
---
# <a name="bug-check-0x17e-microcoderevisionmismatch"></a>バグ チェック 0x17E の。マイクロ コード\_リビジョン\_が一致しません

マイクロ コード\_リビジョン\_の不一致のバグ チェックが 0x0000017E の値を持ちます。 これは、マルチプロセッサの構成で 1 つまたは複数のプロセッサに一貫性のないマイクロ コードが読み込まれるがあることを示します。  

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。

 

## <a name="microcoderevisionmismatch-parameters"></a>マイクロ コード\_リビジョン\_不一致パラメーター

|パラメーター|説明|
|-------- |---------- |
|1| プロセッサが一致しないプロセッサの CPUID 署名値。 |
|2| プロセッサの予想されるマイクロ コード リビジョン。 |
|3| 実際、プロセッサのマイクロ コード リビジョンを報告します。 |
|4| 一致していないプロセッサのプロセッサのインデックス。|


## <a name="cause"></a>原因
-----
マルチプロセッサの構成で 1 つまたは複数のプロセッサでは、読み込まれる一貫性のないマイクロ コードがあります。 このバグチェックでは、その問題のあるシステム ファームウェアがホストの構成内のプロセッサのサブセットのみにマイクロ コードの更新プログラムを適用誤ってことを示します。 システム ファームウェアでは、統一された方法ですべてのプロセッサにマイクロ コードの更新プログラムを適用する必要があります。 

## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

