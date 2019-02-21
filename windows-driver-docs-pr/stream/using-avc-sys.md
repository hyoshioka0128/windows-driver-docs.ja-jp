---
title: Avc.sys を使用します。
description: Avc.sys を使用します。
ms.assetid: 3b4ec139-ff01-40bd-8e29-92f554180585
keywords:
- Avc.sys 関数ドライバーに関する Avc.sys 関数ドライバー WDK、
- AV/C WDK、Avc.sys 使用状況
- サブユニット サポート WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22cc329213f0ce766e2feb1ea6d394ee1debe16a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552123"
---
# <a name="using-avcsys"></a>Avc.sys を使用します。





Windows の後にロードし、初期化*Avc.sys*、 *Avc.sys* (いずれかを含む IEEE 1394 バスに接続されている使用標準 AV/C 単体テストとサブユニット コマンド AV/C のすべてのデバイスで作業中のサブユニットを検出するには仮想のサブユニット コンピューターが仮想 AV/C 単位)。 *Avc.sys* active サブユニットのすべてのデバイス識別子 (Id) を生成します。 次に、 *Avc.sys*各サブユニットのサブユニットを適切なドライバーの読み込み、標準のプラグ アンド プレイ (PnP) メカニズムを使用します。 によって生成される、サブユニット ドライバーおよびサブユニットのデバイス識別子をインストールする INF ファイルに基づくサブユニット ドライバーが読み込まれるが選択されて*Avc.sys* 「 [AV/C デバイス Id](av-c-device-identifiers.md)します。 ユニットの情報のサブユニットのと組み合わせて、AV/C デバイスからデバイス id が生成された***SubunitType***と***SubunitID***フィールド。 サブユニットをサポートするドライバーはベンダー固有かサブユニットの型のジェネリックであることができます。 ほとんどのデジタル ビデオ_カメラのサブユニット ドライバーは、Microsoft のなど*Msdv.sys*します。

サブユニット ドライバーとの通信*Avc.sys* WDM アーキテクチャに基づくすべてのドライバーで採用されている標準の IRP に基づくメカニズムを通じてします。 サブユニット ドライバーはの割り当てと、AV/C プロトコル ドライバーをドライバー スタック ダウン Irp を送信してその AV/C サブユニットと通信*Avc.sys*します。 I/O 要求を行うには、ヘッダー ファイルをインクルード*Avc.h*、これで、Microsoft Windows Driver Kit (WDK) に付属しています。

サブユニット ドライバーは、初期化によって処理される Irp *Avc.sys*します。 サブユニット ドライバーの設定の IRP **Parameters.DeviceIoControl.IoControlCode** IOCTL AV/C の目的の操作に対応するメンバー。

*Avc.sys* 2 つのいずれかの登録[デバイス インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff543137)に読み込まれたどのサブユニット ドライバー スタックによって、サポート (ピアまたは仮想)。 これらのインターフェイスは、機能を定義する*Avc.sys*サブユニット ドライバーのエクスポート、他のドライバー、およびアプリケーションを使用します。 *Avc.sys*有効または無効、ドライバーの PnP 状態に応じて、インターフェイスの状態を変更します。

*Avc.sys* GUID の新しいインスタンスを登録します\_AVC\_クラスの外部の AV/C サブユニット (ピア スタック) のサポートを提供する読み込まれた場合。 このインターフェイスには、次の I/O 制御 (IOCTL) コードのみがサポートされています。

-   [**IOCTL\_AVC\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560789)

IOCTL\_AVC\_クラスは、複数の関数コードをさらにサポートします。 インスタンスの子ドライバー *Avc.sys*がその親のデバイス オブジェクトを使用して、このインターフェイスにアクセスをサポートするピアのサブユニットが保証されます。

GUID\_AVC\_クラス インターフェイスは、すべての IOCTL をサポートしている\_AVC\_関数コードでは、各関数のリファレンス ページ」の説明に従って、利用に関する制限事項があるクラスします。

*Avc.sys* GUID の新しいインスタンスを登録します\_仮想\_AVC\_クラス、仮想 AV/C サブユニット (仮想スタック) のサポートを提供する、読み込まれた場合。 このインターフェイスには、次の 4 つの I/O 制御 (IOCTL) コードがサポートされています。

-   [**IOCTL\_AVC\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560789)

-   [**IOCTL\_AVC\_UPDATE\_仮想\_サブユニット\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560798)

-   [**IOCTL\_AVC\_削除\_仮想\_サブユニット\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560793)

-   [**IOCTL\_AVC\_BUS\_RESET**](https://msdn.microsoft.com/library/windows/hardware/ff560783)

GUID\_仮想\_AVC\_クラス インターフェイスはすべて IOCTL をサポートしていません\_AVC\_クラス関数のコード。 個々 の関数の各コードのリファレンス ページでは、GUID にサポートされているかどうかを指定します\_仮想\_AVC\_クラスのインスタンスの*Avc.sys*します。

IOCTL\_AVC\_クラス Irp がカーネル モード (通常はドライバーの通信) でを通じてのみサポートされて[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)します。 そのため、アプリケーションには、IOCTL によって提供される関数がアクセスできない直接\_AVC\_クラス IOCTL コード。

最後の 3 つの IOCTL コードがカーネル モードとからのユーザー モードの両方でサポートされて[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)します。 つまりがアプリケーションを送信できるこれらの Ioctl に直接*Avc.sys*します。

IOCTL\_AVC\_クラス IOCTL コードは、実行する C AV/操作の詳細を説明する I/O 要求ブロック (IRB) では常に伴う必要があります。 IRB ヘッダーには、IRB の残りの部分の構造が決まり、関数の数が含まれています。 サイズと IRB 構造体は、関数によって異なります。 *Avc.sys* 2 つのカスタム IRBs を使用します。

-   [**AVC\_コマンド\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554140)

-   [**AVC\_MULTIFUNC\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554177)

これを選択 IRB サブユニット ドライバーを使用する必要がありますは、必要な関数に依存します。 詳細については、IOCTL\_AVC\_クラスの関数コードでサポートされている*Avc.sys、* を参照してください[AV/C プロトコル ドライバー関数コード](https://msdn.microsoft.com/library/windows/hardware/ff556389)。

サブユニット ドライバーによって使用されるプライマリ AV/C 関数は[ **AVC\_関数\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/ff554150)、使用、AVC\_コマンド\_IRB 構造体。 **AVC\_関数\_コマンド**AV/C を要求して、対応する C AV/応答の受信を送信します。 AV/C コマンドを構築するための詳細については、 *Avc.sys*AV/C オペコードと各コマンドのオペランドのサブユニット ドライバーが提供する必要があります。

 

 




