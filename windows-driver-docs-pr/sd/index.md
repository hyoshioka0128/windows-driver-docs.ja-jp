---
title: SD バス ドライバー設計ガイド
description: SD バス ドライバー設計ガイド
ms.assetid: c082d86c-8f81-41ef-afac-bd9fd76696fd
keywords:
- SD WDK バス
- バス WDK, SD
- セキュア デジタル WDK バス
- メモリ カード WDK SD バス
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
author: EliotSeattle
ms.openlocfilehash: 52b8d72daa37b4e369da27c63f61552dea54569c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824742"
---
# <a name="sd-bus-driver-design-guide"></a>SD バス ドライバー設計ガイド

[SD カードのドライバー スタック](https://docs.microsoft.com/windows-hardware/drivers/sd/sd-card-driver-stack)

[SD カードのバス インターフェイスを開く、初期化する、および閉じる](https://docs.microsoft.com/windows-hardware/drivers/sd/opening--initializing-and-closing-an-sd-card-bus-interface)

[SD カードの割り込みの処理](https://docs.microsoft.com/windows-hardware/drivers/sd/handling-sd-card-interrupts)

[SD カードの要求](https://docs.microsoft.com/windows-hardware/drivers/sd/sd-card-requests)

## <a name="sd-card-hardware-identifiers"></a>SD カードのハードウェア識別子

セキュア デジタル (SD) デバイスの ID 文字列の詳細については、「[Identifiers for Secure Digital (SD) Devices (セキュア デジタル (SD) デバイスの識別子)](https://docs.microsoft.com/windows-hardware/drivers/install/identifiers-for-secure-digital--sd--devices)」をご覧ください。

## <a name="restrictions-on-sd-card-drivers"></a>SD カード ドライバーに関する制限事項

SD コンボ (多機能) カード上の関数を管理するセキュア デジタル (SD) カードのデバイス ドライバーには、特定の制限事項が適用されます。 多機能カード上のさまざまなカード関数に対応するドライバー スタックは、互いに独立して動作する必要があります。 この独立性を確保するために、バス ドライバーは次の操作を拒否します。

- デバイスの状態を変更する SD コマンド (SELECT\_CARD など)。

- 関数ゼロを指定し、Function Basic Register (FBR) に指定されたアドレスの範囲外にある SD I/O コマンド。

- 別のデバイス スタックの関数番号を指定する SD I/O コマンド。

SD デバイス ドライバーでは、型 SDRF\_GET\_PROPERTY および SDRF\_SET\_PROPERTY の関数要求を使用して [**SdBusSubmitRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbussubmitrequest) を呼び出すことで、ホスト コントローラーの一般的なレジスタ セットとデバイスの状態を管理できます。 これらの関数要求の型の説明については、「[**SD\_REQUEST\_FUNCTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/ne-ntddsd-sd_request_function)」をご覧ください。

## <a name="sd-bus-sample"></a>SD バスのサンプル

これは、動作しているセキュア デジタル (SD) IO ドライバーのサンプルです。 このドライバーは、カーネルモード ドライバー フレームワークを使用して作成されます。 これは、SDIO プロトコルを実装する汎用の mars 開発ボード向けのドライバーです。追加機能はありません。

GitHub から[記憶域の SDIO ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617953)をダウンロードしてください。
