---
title: WMI データ ブロックとイベント ブロックの設計
description: WMI データ ブロックとイベント ブロックの設計
ms.assetid: 3235accd-2bec-430e-ab00-1c5d0ef46045
keywords:
- WMI の WDK カーネルでは、イベント ブロック
- イベントは、WDK の WMI をブロックします。
- WDK の WMI のデータ ブロックします。
- WMI の WDK カーネルでは、データのブロック
- WDK の WMI をブロックします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9562f66b1302add7a4c29fdd37367156110a343b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388184"
---
# <a name="designing-wmi-data-and-event-blocks"></a>WMI データ ブロックとイベント ブロックの設計





最適なパフォーマンスと使いやすさを WMI クライアント、ドライバーは、標準的なデータのブロックをサポートする必要があり、ドライバー開発者がカスタムの WMI データとイベントのブロックの設計で特定のガイドラインに従う必要があります。 具体的には、ドライバーの作成者は、パフォーマンスのトレードオフを選択するデータ ブロックの動的インスタンス名と静的認識する必要があります。 このセクションのトピックでは、問題と WMI のデータとイベントのブロックを設計するためのガイドラインについて説明します。

 

 




