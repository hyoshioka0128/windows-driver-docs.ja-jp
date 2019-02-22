---
title: 書き込み WDM ドライバー
description: 書き込み WDM ドライバー
ms.assetid: 379305f0-3caa-4c8d-add5-17e8c83f2429
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b894bcff2e80d3fa24cb2168164efe883632349
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531357"
---
# <a name="writing-wdm-drivers"></a>書き込み WDM ドライバー


このセクションでは、Microsoft Windows Driver Model (WDM) アーキテクチャについて説明します。 このアーキテクチャは、前の Windows NT のデバイス ドライバーへの機能拡張としては、Windows 2000 で起動しました。

**注**  ドライバーのバージョンの Windows NT ベースのオペレーティング システム、Windows 2000 がサポートされていないと、これらのドライバーを更新する必要があります前にします。 (Windows 98) などのオペレーティング システムの非 Windows NT ベースのドライバーが WDM アーキテクチャではサポートされていないし、このようなドライバーを書き直す必要があります。

 

このセクションでは、3 つの部分に分かれています。

-   [Windows Driver Model](windows-driver-model.md) WDM ドライバー、デバイスの構成、および WDM バージョン管理の種類を含む Windows Driver Model (WDM) について説明します。

-   [デバイス オブジェクトとデバイス スタック](device-objects-and-device-stacks.md)デバイス オブジェクトとデバイス スタックについて説明します。 セクションには、物理デバイス オブジェクト (Pdo)、機能のデバイス オブジェクト (Fdo)、およびデバイス オブジェクトをフィルター (フィルター DOs) に関する情報が含まれています。 ドライバーは、連携して動作するデバイス オブジェクトのセットから多くの場合、構築されます。 この一連のデバイス オブジェクトが呼び出されます、*スタック*します。 スタックに情報の流れを把握し、内部的にドライバーとドライバーの方法のさまざまな部分から通信できます。

-   [カーネル モード ドライバー コンポーネント](kernel-mode-driver-components.md)ドライバーが機能するために実装する必要があります、ルーチンは省略可能なルーチンをについて説明します。

    A*デバイス ドライバー*オペレーティング システムに統合する必要があるソフトウェアのコードのセットです。 この統合を完了するには、必要があります、ハンドラー ルーチンのセットをドライバーで記述するプロセスが、オペレーティング システムから呼び出すことです。 これらのルーチンは、単純な関数呼び出しを指定できますが、それらの多くの処理を実装*I/O 要求パケット*(Irp) ドライバーとオペレーティング システム間の通信を容易にします。

**注**  WDM ドライバーでは Windows Driver Frameworks (WDF) ライブラリを記述するデバイス ドライバーの一部を簡単にも使用できます。 具体的には、カーネル モード ドライバーでは、カーネル モード ドライバー フレームワーク (KMDF) WDF の一部であるを使用できます。 カーネル モード ドライバー用 KMDF の詳細については、次を参照してください。[カーネル モード ドライバー フレームワークの概要](https://msdn.microsoft.com/library/windows/hardware/ff544296)します。 KMDF に WDM が置き換えられることに注意してください。 まだ WDM、KMDF ドライバーを作成するの多くの部分を理解しておく必要があります。

 

 

 




