---
title: Windows Device Testing Framework (WDTF) 設計ガイド
description: Microsoft Windows Device Testing Framework (WDTF) を使用すると、デバイスを中心としたシナリオ ベースの自動テストを作成、管理、再利用、および拡張できます。
ms.assetid: cff552f0-5dde-4fe7-996c-0a496d845edc
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
author: EliotSeattle
ms.openlocfilehash: b6b806bc280491d8d92382898310167c5dcda855
ms.sourcegitcommit: 85d02ecf7cbcfd802f41f68cea4cd4434284bdaa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68473556"
---
# <a name="windows-device-testing-framework-wdtf-design-guide"></a>Windows Device Testing Framework (WDTF) 設計ガイド

Microsoft Windows Device Testing Framework (WDTF) を使用すると、デバイスを中心としたシナリオ ベースの自動テストを作成、管理、再利用、および拡張できます。

## <a name="in-this-section"></a>このセクションの内容

|トピック|説明|
|----|----|
|[デバイス用の WDTF シンプル IO プラグインの作成](writing-a-wdtf-simpleio-plug-in-for-your-device.md)|[デバイスの基本テスト](https://docs.microsoft.com/windows-hardware/drivers)のメリットを最大限に引き出すには、デバイスへのシンプル I/O を実行できるシンプル I/O プラグインがデバイスに必要です。 これには、WDTF に付属する既定のいずれかのシンプル I/O プラグまたはユーザーが作成した I/O プラグを使用できます。 デバイスの種類がサポートされているかどうかと、テストに固有の要件があるかどうかを確認するには、「[提供されている WDTF シンプル I/O プラグイン](provided-wdtf-simpleio-plug-ins.md)」をご覧ください。|
|[WDTF を使用したテストの作成](writing-tests-with-wdtf.md)|Windows Driver Kit (WDK) で提供されるテンプレートを使用してドライバー テストの作成を開始する場合、または独自にテストを作成する場合のどちらでも、Microsoft Windows Device Testing Framework (WDTF) を使用すると、デバイスを中心としたシナリオ ベースの自動テストを作成および拡張できます。|
|[WDTF ベースのテストのトリアージ](triaging-wdtf-based-tests.md)|WDTF ベースのテストで行われる内容についての理解を深めるために、[WDTF オブジェクト ログ](logging-and-tracing.md)および [WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)の組み込みのサポートを使用できます。|
|[WDTF アーキテクチャと概要](wdtf-overview.md)|Microsoft Windows Device Testing Framework (WDTF) を使用すると、デバイスを中心としたシナリオ ベースの自動テストを作成、管理、再利用、および拡張できます。|
