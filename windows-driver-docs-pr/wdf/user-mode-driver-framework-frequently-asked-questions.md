---
title: ユーザー モード ドライバー フレームワークについてよく寄せられる質問
description: Windows ドライバーフレームワーク (WDF) は、Windows オペレーティングシステムで実行されるデバイスドライバーの作成に使用できる一連のライブラリです。
ms.assetid: 0c07e514-73f9-4d24-86ad-8ac036fdbcf4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e78ac468915748ce2076f5075b83626a59b1b52
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843103"
---
# <a name="user-mode-driver-framework-frequently-asked-questions"></a>ユーザー モード ドライバー フレームワークについてよく寄せられる質問


Windows ドライバーフレームワーク (WDF) は、Windows オペレーティングシステムで実行されるデバイスドライバーの作成に使用できる一連のライブラリです。 WDF は、カーネルモードドライバーフレームワーク (KMDF) とユーザーモードドライバーフレームワーク (UMDF) の2つのフレームワークによってサポートされる単一のドライバーモデルを定義します。 このトピックでは、UMDF に関してよく寄せられる質問に対する回答を示します。

## <a name="which-operating-systems-can-run-umdf-drivers"></a>UMDF ドライバーを実行できるオペレーティングシステムを教えてください。


UMDF ドライバーは、次のオペレーティングシステムで実行できます。

-   Windows 10
-   Windows 8.1
-   Windows 8
-   Windows 7
-   Windows Vista
-   Windows XP

## <a name="what-is-the-most-recent-version-of-umdf"></a>最新バージョンの UMDF はどのようなものですか。


Windows 10 以降には、UMDF version 2 (2.0 と2.1 の両方) が含まれています。

## <a name="what-is-the-difference-between-umdf-version-2-and-the-previous-version-111-one-dot-eleven"></a>UMDF version 2 と以前のバージョン 1.11 (1 つのドット 11) の違いは何ですか。


UMDF version 2 で記述されたドライバーは、C プログラミング言語で記述されています。 この同じドライバーを KMDF 用に簡単にコンパイルできます。 また、UMDF version 1 ドライバーは、COM プログラミングモデルに従って記述されている必要があります。 

詳細については、「[はじめにと UMDF](getting-started-with-umdf-version-2.md)」を参照してください。

## <a name="which-operating-systems-support-umdf-2"></a>UMDF 2 をサポートするオペレーティングシステム


UMDF version 2 ドライバーは Windows 8.1 以降で実行されます。

## <a name="which-umdf-versions-can-i-build-against-in-windows-driver-kit-wdk10"></a>Windows Driver Kit (WDK) 10 ではどのようなバージョンの UMDF を構築できますか。


Windows Driver Kit (WDK) 10 および Microsoft Visual Studio を使用して、UMDF 2.1、2.0、1.11、および1.9 のドライバーをビルドできます。 これらの UMDF バージョンを使用してビルドされたドライバーを実行できる Windows のバージョンについては、「 [Umdf Version History](umdf-version-history.md)」を参照してください。

## <a name="can-i-write-part-of-my-driver-to-run-in-user-mode-and-part-in-kernel-mode"></a>ドライバーの一部をユーザーモードで実行し、カーネルモードで実行することはできますか。


できます。 ドライバーがカーネルモードのリソースや機能にアクセスする必要がある場合でも、ドライバーを2つの部分に分割することができます。 この方法では、ユーザーモードでのドライバーの開発と実行の利点の一部を活用できます。

UMDF ドライバーは、カーネルモードドライバーから i/o 要求を受け取ることができます。 *カーネルモードクライアント*の詳細については、「 [UMDF 2 ドライバーでのカーネルモードクライアントのサポート](supporting-kernel-mode-clients-in-umdf-drivers.md)」を参照してください。

ただし、KMDF と UMDF の間のパリティが増加した結果として、ドライバーを分割する必要が生じることはほとんどありません。

##  <a name="which-framework-should-i-start-with"></a>最初にどのフレームワークを使用する必要がありますか。


「 [UMDF 2 機能を KMDF と比較](comparing-umdf-2-0-functionality-to-kmdf.md)する」に記載されている、あまり一般的でない機能がドライバーで必要な場合は、kmdf を使用する必要があります。 他のすべてのドライバーについては、最初の選択は UMDF にする必要があります。

UMDF から開始し、後で KMDF への移行を決定する場合は、「 [kmdf ドライバーを UMDF 2 ドライバーに変換する方法 (およびその逆)](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)」で説明されているように、最小限の労力でこれを行うことができます。

## <a name="how-do-user-mode-drivers-handle-security"></a>ユーザーモードドライバーはセキュリティをどのように処理しますか。


UMDF ドライバーは、LocalService アカウントのセキュリティ資格情報で実行されるドライバーホストプロセスで実行されます。ただし、ホストプロセス自体は Windows サービスではありません。 そのため、ユーザーモードドライバーは、他のユーザーモードサービスと同じようにセキュリティで保護されています。 UMDF ドライバーは、i/o 要求を発行するときに、必要に応じてクライアントプロセスを偽装できます。 偽装により、ドライバーのスレッドをクライアントのセキュリティコンテキストで実行できるようになります。これにより、システムは、ドライバーのホストプロセスではなく、クライアントの id に対してアクセスチェックを実行できるようになります。

ユーザーモードドライバーは、プラグアンドプレイまたはその他のシステムメッセージではなく、i/o 要求に対してのみクライアントプロセスを偽装できます。

ドライバーのインストール時に、INF ファイルによってドライバーの最大偽装レベルが設定されます。 "権限の昇格" 攻撃を防ぐために、できるだけ低いレベルで偽装を設定する必要があります。 クライアントアプリケーションは、 **CreateFile**関数を呼び出すと、偽装レベルを指定します。 ドライバーは、このレベルの偽装を個々の i/o 要求に対して要求します。

## <a name="will-a-user-mode-driver-be-fast-enough"></a>ユーザーモードドライバーは十分に高速ですか。


UMDF の開発では、パフォーマンスが優先されます。 待機時間と CPU 使用率の両方が多少増加しますが、バス容量は、UMDF がサポートするデバイスの種類の主要な要因となります。

## <a name="what-is-the-difference-between-a-user-mode-driver-and-an-application"></a>ユーザーモードドライバーとアプリケーションの違いは何ですか。


ユーザーモードドライバーは、ドライバーマネージャーによって起動され、ドライバーホストプロセスで実行されます。 ドライバーの1つのインスタンスで、複数のアプリケーションからの同時要求を処理できます。 ドライバーと通信するために、アプリケーションは Win32 API を通じて、ドライバーのデバイスに i/o 要求を発行します。 ユーザーモードドライバーのプライマリエントリポイントは、 **main ()** 関数ではなく、 [**Idriverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)インターフェイス (umdf 1.11 以前) または[**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチン (umdf 2.0 以降) です。

また、ドライバーには、i/o 要求とプラグアンドプレイおよび電源通知への応答として呼び出される、追加のインターフェイスまたはコールバックも含まれます。 UMDF ドライバーによって管理されるデバイスは、システムに統合され、プラグアンドプレイと電源管理に参加します。

## <a name="how-do-i-debug-a-umdf-driver"></a>UMDF ドライバーをデバッグ操作方法には


ユーザーモードのデバッガーまたはカーネルモードのデバッガーを使用して、UMDF ドライバーをデバッグできます。 詳細については、「 [WDF ドライバーのデバッグ](debugging-a-wdf-driver.md)」を参照してください。

UMDF バージョン2.0 以降では、 *Wdfkd*デバッガー拡張ライブラリの多くのコマンドを使用して、umdf ドライバーをデバッグできます。 コマンドの一覧については、「[デバッガーの拡張機能](debugger-extensions-for-kmdf-drivers.md)」を参照してください。 また、umdf は、UMDF トレースログ (または UMDF *IFR*) をカーネル非ページメモリに格納します。 IFR の詳細については、「[フレームワークのイベントロガーの使用](using-the-framework-s-event-logger.md)」を参照してください。

## <a name="is-there-a-newsgroup-for-umdf"></a>UMDF のニュースグループはありますか。


Windows ドライバーのすべての側面については、次のフォーラムを参照してください。

-   Microsoft は、 [Windows HARDWARE WDK およびドライバー開発](https://social.msdn.microsoft.com/Forums/windowsdesktop/home?forum=wdk)フォーラムを管理しています。

-   [Osr オンライン NTDEV List](https://community.osr.com/)フォーラムで、システムリソース (osr) 軽減を開きます。

 

 





