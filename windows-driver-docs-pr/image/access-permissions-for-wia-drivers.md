---
title: WIA ドライバーへのアクセス許可
description: WIA ドライバーへのアクセス許可
ms.assetid: 593e9367-5304-4b04-8597-4a7c498b9f47
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4e7358e254013db4b48becc17d9bf83359ee9135
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377632"
---
# <a name="access-permissions-for-wia-drivers"></a>WIA ドライバーへのアクセス許可

同じ名前のオブジェクトを使用するドライバーと他のコンポーネントの順序は作成時に適切なアクセス許可オブジェクトの設定する必要があります。 通常、そのオブジェクトのセキュリティ記述子で適切な DACL を設定が含まれます。

これを行う簡単な方法では、セキュリティ記述子定義言語 (SDDL) 関数を使用します。 SDDL は Windows セキュリティ記述子、または SD. の単純な文字列表現であります。 SDDL 文字列を SD を変換できるし、SDs を 2 つのセキュリティ記述子を比較するために役立つ SDDL 文字列に変換できます。

SDDL を使用して、イベント オブジェクトのアクセス許可を設定する例は、次を参照してください。 [WIA セキュリティおよびセキュリティ記述子](wia-security-and-security-descriptors.md)します。

