---
title: ビデオのミニポート ドライバーのバグ チェックのデータの最大サイズ
description: ビデオのミニポート ドライバーのバグ チェックのデータの最大サイズを指定します。
ms.assetid: 1644fe85-b5f5-44b5-96b7-258f43607171
keywords:
- BugcheckDataSize
- ビデオのミニポート ドライバーのバグ チェック データ WDK DirectX 9.0
- バグ チェックでデータのサイズを WDK DirectX 9.0
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 5505f45a4d2bb32dd9c3394a8da1aa383fcf71a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557051"
---
# <a name="the-max-size-of-bug-check-data-in-a-video-miniport-driver"></a>ビデオのミニポート ドライバーのバグ チェックのデータの最大サイズ


**このトピックでは、Microsoft Windows XP Service Pack 1 (SP1) 以降にのみ適用されます。**

ビデオのミニポート ドライバーの値を設定する必要があります、 *BugcheckDataSize*のパラメーター、 **VideoPortRegisterBugcheckCallback**関数を Windows XP sp1 0x0F20 (4000) のバイトを超えるとMicrosoft Windows Server 2003 を解放します。 Windows Server 2003 およびそれ以降のリリースでは、最大の値の*BugcheckDataSize*は、最大\_セカンダリ\_ダンプ\_定数のサイズ。 この定数の値は、Windows Server 2003 以降のリリースで変更可能性があります。

Windows XP SP1 DDK ドキュメントでの最大値が正しく指定されて*BugcheckDataSize*します。

 

 





