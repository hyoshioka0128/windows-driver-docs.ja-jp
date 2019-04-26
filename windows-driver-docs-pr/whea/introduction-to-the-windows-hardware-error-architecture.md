---
title: Windows Hardware Error Architecture (WHEA) の概要
description: Windows Hardware Error Architecture (WHEA) の概要
ms.assetid: 5a0bbf8c-d644-4a64-9a7e-400d5de2c8fa
keywords:
- Windows Hardware Error Architecture WDK は、Windows Hardware Error Architecture について
- Windows Hardware Error Architecture について、WHEA WDK
- Windows Hardware Error Architecture についての WDK WHEA のハードウェア エラー
- Windows Hardware Error Architecture についての WDK WHEA エラー
- ソース情報 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e566a3c14b9ab758a26f09b7ef8766b47f1a30f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340778"
---
# <a name="introduction-to-the-windows-hardware-error-architecture"></a>Windows Hardware Error Architecture の基本


Windows Vista より前に、Microsoft Windows オペレーティング システムのバージョンでは、オペレーティング システムは、ハードウェア エラーの報告関連のないいくつかのメカニズムをサポートします。 これらのメカニズムでは、エラー回復のほとんどのサポートが用意されています。 未修正のエラーは、オペレーティング システムは、だけのバグ チェックが生成され、使用可能なエラー情報の一部のシステム イベント ログに記録、システムの再起動後です。

ハードウェア エラーの根本原因を特定する機能の障害は、限られた量のシステム イベント ログに記録されたエラー情報になります。 オペレーティング システムが共通がなかったので、ハードウェア エラーによって発生するシステムのクラッシュを防止できるエラー レコードの形式とハードウェア エラー管理アプリケーションのサポートがほとんどありません。

Windows ハードウェア エラー アーキテクチャ (WHEA)、Windows Vista で導入されたは、ハードウェア エラーの前のレポート メカニズムを拡張し、一貫性のあるハードウェア エラー インフラストラクチャのコンポーネントとして一緒に置きます。 WHEA では、今日のハードウェア デバイスで使用できる追加のハードウェア エラーの情報を利用し、システム ファームウェアとより密接に統合します。

その結果、WHEA では、次の利点があります。

-   ハードウェア エラーの根本原因を判断するための標準エラー レコードの形式で使用可能にするより広範なエラー データは、できます。

-   支援するためのメカニズムを提供します。 バグを回避するためにハードウェア エラーから回復、ハードウェア エラーが致命的でない場合に確認してください。

-   エラー管理アプリケーションのユーザー モードをサポートし、Event Tracing for Windows (ETW) イベントとエラー管理および制御するための API を提供することで、高度なシステムの正常性監視を有効にします。

-   WHEA により新しいメカニズムを適切に対応するために、オペレーティング システム、ハードウェア ベンダーは、新しいハードウェア エラーの報告メカニズムに自分のデバイスを追加するにようには、拡張性を提供します。

 

 




