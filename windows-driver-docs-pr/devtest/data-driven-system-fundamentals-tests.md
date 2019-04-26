---
title: データ ドリブンのシステムの基本テスト
description: システムの基本テストと Windows ドライバー関連のユーティリティの概要
keywords:
- Sysfund テスト
- データ ドリブン テスト
ms.date: 06/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: e66284eaf9a04f5e90af4c1d90ad81b7f601fb0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356612"
---
# <a name="data-driven-system-fundamentals-tests"></a>データ ドリブン システムの基本テスト

マイクロソフトとエンタープライズ WDK (EWDK) 1703 以降では、構成可能なコマンド ライン バージョンのシステムの基本テストと関連付けられているユーティリティを提供します。  これらは、「データドリブン」テストおよびユーティリティと呼ばれます。

システムの基礎 (SysFund) のデータ ドリブン テスト構成と XML ファイル (wdtftest.xml) を使用してカスタマイズられ、コマンドラインを使用して実行されます。 テストは、ドライバーとデバイスの開発中に早い段階で頻繁に実行する設計されています。

SysFund のデータ ドリブン テストでは、システムが SysFund のデータ ドリブン テストに渡すことができる場合、HLK 内 SysFund のテストにコードと同じであるため HLK SysFund テストに合格することもする必要があります。 異なり、HLK で SysFund テスト、ただし、SysFund のデータ ドリブン テストは、一連のシステム上のすべてのデバイスに 1 つのデバイスからデバイスを対象に構成できます。  これにより、新しいまたは更新されたデバイスやシステムの反復的なテスト プロセス。
