---
title: バグ チェック 0x18D SECURE_FAULT_UNHANDLED
description: SECURE_FAULT_UNHANDLED のバグ チェックでは、0x0000018D の値を持ちます。 これは、セキュリティで保護されたカーネルによって発生したセキュリティで保護されたフォールトを処理できなかったことを示します。
keywords:
- バグ チェック 0x18D SECURE_FAULT_UNHANDLED
- SECURE_FAULT_UNHANDLED
ms.date: 01/04/2019
topic_type:
- apiref
api_name:
- SECURE_FAULT_UNHANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74c275e9cb45d5790b1b665574559caecf2ad655
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743570"
---
# <a name="bug-check-0x18d-securefaultunhandled"></a>バグ チェック 0x18D の。セキュリティで保護された\_フォールト\_未処理

SECURE\_フォールト\_未処理のバグ チェックが 0x0000018D の値を持ちます。

このセキュリティで保護されたカーネルによって、セキュリティで保護されたエラーが発生したバグ チェック indidates を処理できませんでした。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


 ## <a name="securefaultunhandled-parameters"></a>セキュリティで保護された\_フォールト\_ハンドルされていないパラメーター

| パラメーター | 説明 |
|-----------|-------------|
| 1         | エラー コードのビットマスクの次の値をセキュリティで保護します。 |
| 2         | フォールト VA (特定のセキュリティで保護されたフォールトの型にのみ適用) をセキュリティで保護します。 |
| 3         | 例外レコードです。 |
| 4         | コンテキスト レコード。 |


**エラー コードのビットマスクをセキュリティで保護します。**

     0x1 : KSECURE_FAULT_SLAT_NX
         A no-execute fault occured due to SLAT page protections.
     0x2 : KSECURE_FALT_SLAT_READ
         A read fault occurred due to SLAT page protections.
     0x4 : KSECURE_FAULT_SLAT_WRITE
         A write fault occured due to SLAT page protections.
     0x8 : KSECURE_FAULT_DOUBLE_FAULT
         A secure fault occurred before the prior secure fault had been dismissed by the kernel.

## <a name="cause"></a>原因
-----

セキュリティで保護されたカーネルによって発生したセキュリティで保護されたフォールトを処理できませんでした。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)


 

 




