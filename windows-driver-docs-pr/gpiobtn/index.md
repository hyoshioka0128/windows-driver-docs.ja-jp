---
title: ハードウェア通知設計ガイド
description: 主要なボタン (電源、Windows、ボリューム、回転ロック) とその他のインジケーターの標準化された方法でのサポート、および関連する Windows Engineering Guidance (WEG) について説明します。
ms.assetid: E18DAA6C-C64D-40B3-A112-682A935655D0
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
author: EliotSeattle
ms.openlocfilehash: db7b3cb252174f91e40179c7ea6fc540dee64cfc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824893"
---
# <a name="hardware-notifications-design-guide"></a>ハードウェア通知設計ガイド

主要なボタン (電源、Windows、ボリューム、回転ロック) とその他のインジケーターの標準化された方法でのサポート、および関連する Windows Engineering Guidance (WEG) について説明します。

## <a name="in-this-section"></a>このセクションの内容

|トピック|説明|
|----|----|
|[GPIO のボタンおよびインジケーター実装ガイド](gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md)|Windows 8 では、HID ミニポート クラス ドライバーを使用して、汎用 I/O (GPIO) のボタンとインジケーターのサポートが導入されていました。 その目的は、主要なボタン (電源、Windows、ボリューム、回転ロック) の標準化された方法でのサポート、および関連する Windows Engineering Guidance (WEG) を提供することでした。 Windows 8.1 では、エンド ツー エンドのユーザー エクスペリエンスの品質の向上および革新的なさまざまなフォーム ファクター間での動作の統一に重点を置いています。|
|[GPIO のボタンおよびインジケーターの補足的なテスト](gpio-buttons-and-indicators-supplemental-certification-testing-for-windows-8-1.md)|このトピックでは、さまざまなフォーム ファクターに最適なユーザー エクスペリエンスを確保するための、ハードウェアのボタンとインジケーターに対する Windows 8.1 のテスト シナリオについて説明します。|
|[ハードウェア通知のサポート](hardware-notifications-support.md)|Windows 10 バージョン 1709 には、通知コンポーネント (LED、振動のメカニズムなど) のハードウェアに依存しないサポート用のインフラストラクチャが用意されています。 このサポートは、クライアント ドライバーの迅速な開発を可能にするハードウェア通知コンポーネント専用のカーネルモード ドライバー フレームワーク (KMDF) クラスの拡張を導入することで提供されます。 KMDF クラスの拡張は、本質的には、特定のクラスのデバイス用に定義された機能セットを提供する KMDF ドライバーであり、Windows Driver Model (WDM) 内のポート ドライバーと同様です。 このセクションでは、ハードウェア通知クラスの拡張のアーキテクチャの概要を示します。 KMDF の詳細については、「[Using WDF to Develop a Driver (WDF を使用したドライバーの開発)](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)」をご覧ください。|

## <a name="related-topics"></a>関連トピック

[ハードウェア通知リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
