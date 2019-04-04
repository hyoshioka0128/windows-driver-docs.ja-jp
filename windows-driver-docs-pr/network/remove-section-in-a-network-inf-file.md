---
title: ネットワークの INF ファイルでセクションを削除します。
description: ネットワークの INF ファイルでセクションを削除します。
ms.assetid: c9be4e98-fa35-4966-895a-aebe29f16289
keywords:
- INF ファイル WDK ネットワークの削除
- ネットワーク INF ファイル WDK を削除
- セクションの WDK ネットワークを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e95cf8aecd7d411470c53ed8640c05b154316fdd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551399"
---
# <a name="remove-section-in-a-network-inf-file"></a>ネットワークの INF ファイルでセクションを削除します。





**削除**のセクションではサポートされて**NetClient**、 **NetTrans**、および**NetService**コンポーネントではなく**Net**コンポーネント (アダプター)。

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

ネットワーク クラスのインストーラーを追跡するありませんアダプター インスタンス。 A**削除**を他のアダプターかアダプターの複数のインスタンスを共有するファイルを削除するセクションを表示できるこれらのアダプターまたはアダプター インスタンス動作していません。
かどうかによって使用されるドライバー ファイルを削除する必要が、 **Net**コンポーネント、ファイルを使用しているすべてのドライバーを追跡する共同インストーラーを使用します。 このような共同インストーラーには、同じデバイスに複数のデバイス ドライバーの複数のインスタンスも追跡する必要があります。 共同インストーラーの詳細については、[INF ファイルを作成する](https://msdn.microsoft.com/library/windows/hardware/ff549520)を参照してください。

 

 





