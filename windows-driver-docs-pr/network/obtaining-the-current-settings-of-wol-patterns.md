---
title: WOL パターンの現在の設定の取得
description: WOL パターンの現在の設定の取得
ms.assetid: 113ea75a-83d8-41aa-b61c-711ef90bccca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea292475114e3a8d5e21eca322fb7f02c8e7bb96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324272"
---
# <a name="obtaining-the-current-settings-of-wol-patterns"></a>WOL パターンの現在の設定の取得





後続のドライバーを使用できます、 [OID\_PM\_WOL\_パターン\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff569772)基になるネットワーク アダプターに設定されている wake on LAN (WOL) パターンを列挙するためのクエリ要求の OID。 で、クエリから正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、一覧へのポインター [ **NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768)現在追加 WOL パターンを記述する構造体。 内容については、 **NDIS\_PM\_WOL\_パターン**構造体は、「[の追加と削除 Wake on LAN パターン](adding-and-deleting-wake-on-lan-patterns.md)します。

NDIS 処理 OID\_PM\_WOL\_パターン\_一覧 OID がミニポート ドライバーに代わって要求。 そのため、NDIS ミニポート ドライバーは、OID をサポートする必要はありません\_PM\_WOL\_パターン\_一覧 OID 要求。

 

 





