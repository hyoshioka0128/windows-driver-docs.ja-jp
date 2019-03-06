---
title: SD バス ドライバー設計ガイド
description: SD バス ドライバー設計ガイド
ms.assetid: c082d86c-8f81-41ef-afac-bd9fd76696fd
keywords:
  - SD WDK バス
  - 'バス WDK, SD'
  - セキュア デジタル WDK バス
  - メモリ カード WDK SD バス
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# <a name="sd-bus-driver-design-guide"></a>SD バス ドライバー設計ガイド


## <a name="in-this-section"></a>このセクションの内容
[SD カードのドライバー スタック](https://msdn.microsoft.com/library/windows/hardware/ff537964)

[SD カードのバス インターフェイスを開く、初期化する、および閉じる](https://msdn.microsoft.com/library/windows/hardware/ff537442)

[SD カードの割り込みの処理](https://msdn.microsoft.com/library/windows/hardware/ff537177)

[SD カードの要求](https://msdn.microsoft.com/library/windows/hardware/ff537983)
 

## <a name="sd-card-hardware-identifiers"></a>SD カードのハードウェア識別子


セキュア デジタル (SD) デバイスの ID 文字列の詳細については、「[Identifiers for Secure Digital (SD) Devices (セキュア デジタル (SD) デバイスの識別子)](https://msdn.microsoft.com/library/windows/hardware/ff546279)」をご覧ください。

## <a name="restrictions-on-sd-card-drivers"></a>SD カード ドライバーに関する制限事項


SD コンボ (多機能) カード上の関数を管理するセキュア デジタル (SD) カードのデバイス ドライバーには、特定の制限事項が適用されます。 多機能カード上のさまざまなカード関数に対応するドライバー スタックは、互いに独立して動作する必要があります。 この独立性を確保するために、バス ドライバーは次の操作を拒否します。

-   デバイスの状態を変更する SD コマンド (SELECT\_CARD など)。

-   関数ゼロを指定し、Function Basic Register (FBR) に指定されたアドレスの範囲外にある SD I/O コマンド。

-   別のデバイス スタックの関数番号を指定する SD I/O コマンド。

SD デバイス ドライバーでは、型 SDRF\_GET\_PROPERTY および SDRF\_SET\_PROPERTY の関数要求を使用して [**SdBusSubmitRequest**](https://msdn.microsoft.com/library/windows/hardware/ff537909) を呼び出すことで、ホスト コントローラーの一般的なレジスタ セットとデバイスの状態を管理できます。 これらの関数要求の型の説明については、「[**SD\_REQUEST\_FUNCTION**](https://msdn.microsoft.com/library/windows/hardware/ff538012)」をご覧ください。

## <a name="sd-bus-sample"></a>SD バスのサンプル


これは、動作しているセキュア デジタル (SD) IO ドライバーのサンプルです。 このドライバーは、カーネルモード ドライバー フレームワークを使用して作成されます。 これは、SDIO プロトコルを実装する汎用の mars 開発ボード向けのドライバーです。追加機能はありません。

GitHub から[記憶域の SDIO ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617953)をダウンロードしてください。

 

 




