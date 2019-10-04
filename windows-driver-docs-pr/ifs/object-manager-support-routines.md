---
title: オブジェクトマネージャーのサポートルーチン
description: オブジェクトマネージャーのサポートルーチン
ms.assetid: 64dc1cfb-faf6-4fe0-a8d9-99f6da6d59b7
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3ff5f70d40fc756b179073985c24fe2a5e2f7132
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955820"
---
# <a name="object-manager-support-routines"></a>オブジェクトマネージャーのサポートルーチン

次の表は、システムによって提供されるオブジェクト管理のサポートルーチンのうち、カーネルモードのファイルシステムとファイルシステム (ミニフィルターおよびレガシ) フィルタードライバーで使用できるものの一部を示しています。システムで使用するために予約されています。 これらのルーチンは、デバイスドライバーでは使用できません。

ここに記載されているルーチンに加えて、ファイルシステムとファイルシステムフィルタードライバーは、カーネルモードドライバーアーキテクチャリファレンスで記述され、 *ntifs*で宣言されているすべての**Ob**_Xxx_ルーチンを呼び出すこともできます。

**ヘッダーファイル:** *ntifs*

** プレフィックス:Ob @ no__t-0_Xxx_

| 関数またはマクロ | 説明 |
| ----------------- | ----------- |
| **ObInsertObject** | システム用に予約されています。 |
| **Obisカーネルハンドル** | 指定されたハンドルがカーネルハンドルであるかどうかを判断します。 |
| **Obmake一時オブジェクト** | システム用に予約されています。 |
| **Oboの Objectbypointer** | ポインターによって参照されるオブジェクトを開き、オブジェクトへのハンドルを返します。 |
| **ObQueryNameString** | 呼び出し元がポインターを持つ特定のオブジェクトの名前を指定します (存在する場合)。 |
| **ObQueryObjectAuditingByHandle** | システム用に予約されています。 |
