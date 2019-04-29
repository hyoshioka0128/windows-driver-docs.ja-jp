---
title: ローカル プリンター接続のテスト
description: ローカル プリンター接続のテスト
ms.assetid: 08a16c04-fc64-4e19-b7f2-7a078bc151a2
keywords:
- ドライバー WDK プリンターのテスト
- プリンター ドライバー、WDK のテスト
- ローカル プリンターを WDK のテスト
- WDK プリンターの接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b3869382216cc8c764a204ac4bc2266eeae9a2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388054"
---
# <a name="testing-local-printer-connectivity"></a>ローカル プリンター接続のテスト


このセクションでは、ローカルで接続されているプリンターの接続をテストする方法に関する一般的なガイドラインを提供します。 バスまたはポートの本質的な性質によりいくつかの原則が当てはまらない場合がありますが、バスまたは印刷デバイスの場合は、接続先ポートにこれらの原則を適用できます。

**注**  次の情報は、Microsoft Windows XP でのテストについて説明します。 コントロール パネル アプリケーションやメニューのオプションなど、他のオペレーティング システムのバージョンの機能は、若干異なる可能性があります。

 

### <a name="setting-up-device-testing"></a>デバイスのテストの設定

デバイスのすべてのテストと次に進む前に設定する、デバッグ セッションを次のように、問題が発生する可能性をキャッチするを確認します。 参照してください[スプーラー コンポーネントのプリンター ドライバーのデバッグと](debugging-printer-drivers-and-spooler-components.md)テスト環境を正しく設定する方法。

1.  既定の設定を有効になっている、Spoolsv.exe を監視すると、Application Verifier を設定します。 さまざまなハードウェアでテストを 32 ビットおよび 64 ビットのマシンを含む推奨します。

2.  Driver Verifier ツールを使用すると、使用しているすべてのカーネル モード ドライバーを監視できます。 プリンター ドライバーでは、必ず Win32k.sys を含める。 参照してください[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)については、ツールを使用して、テスト環境を設定します。

3.  電源管理のテストの前に、デバイスが接続されている場合、確認、テスト環境がすべての可能なシステム電源の状態をサポートしていると、デバイスが入力し正常にすべての状態から復帰できます。

次のセクションでは、ポートに接続されたデバイスをテストするときに、アドレスに、一般的なテスト シナリオをについて説明します。

-   [デバイスのインストール](device-installation.md)

-   [デバイスの機能](testing-device-functionality.md)

-   [デバイス エラーの状態](device-error-states.md)

-   [電源管理](power-management.md)

-   [ストレス テスト](stress-testing.md)

 

 




