---
title: クラッシュダンプフィルタードライバーの概要
description: クラッシュ ダンプ フィルター ドライバー
ms.assetid: d91c00d7-ad17-4fa8-9e78-fee0698d9049
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 51795c1f0025a6f87a5933b0826c770fe40786c1
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606442"
---
# <a name="introduction-to-crash-dump-filter-drivers"></a>クラッシュダンプフィルタードライバーの概要

Windows Vista Service Pack 1 (SP1) および Windows Server 2008 以降のオペレーティングシステムでは、クラッシュダンプインターフェイスの有用性を拡張するために、クラッシュダンプドライバースタックでフィルタードライバーのサポートを定義しました。

クラッシュダンプドライバーは、一般的なランタイムストレージドライバースタックを使用して、ダンプデータをディスクに書き込みません。 クラッシュダンプドライバースタックにフィルタードライバーのサポートを追加することで、カーネルを変更することなく新しい機能を追加できます。 たとえば、休止状態またはクラッシュダンプファイルの内容を暗号化することが可能になります。
