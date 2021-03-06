---
title: 強化されたポイント アンド プリントを使いこなす
description: 更新済みのプリンターの共有メカニズムは拡張されたポイント アンド プリントと呼ばれます、印刷クライアント製造元で提供されるデバイス ドライバーをプリント サーバーからダウンロードすることがなく v4 共有に印刷することができます。
ms.assetid: AD01AAD1-B209-419A-B73B-CA746F1B772A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a791b6b9c0c6ae788da290968f6686a27566926d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366534"
---
# <a name="working-well-with-enhanced-point-and-print"></a>強化されたポイント アンド プリントを使いこなす


更新済みのプリンターの共有メカニズムは拡張されたポイント アンド プリントと呼ばれます、印刷クライアント製造元で提供されるデバイス ドライバーをプリント サーバーからダウンロードすることがなく v4 共有に印刷することができます。

プリント サーバーに接続するときにクライアント コンピューターがドライバー パッケージ全体をダウンロードしないため、点が強化されると、印刷と v4 プリンター ドライバーは、次のアーキテクチャののでご注意ください。 この情報は開発し、v4 プリンター ドライバーを適切にパッケージ化に役立ちます。

## <a name="windows-8-client-connection-behavior"></a>Windows 8 クライアント接続動作


Windows 8 クライアントは、v4 プリンター ドライバーを使用している共有の印刷キューに接続するとき、クライアントはクライアント側のレンダリングをサポートするドライバーを入手しようとします。 クライアントは、サーバーのドライバーの PrinterDriverID に一致する HardwareID でドライバーをローカル DriverStore を検索します。 見つかると、そのドライバーがローカルにインストールされます。 それ以外の場合、クライアントは、強化されたポイント アンド プリント ドライバーを使用して接続します。

どちらの場合は、クライアントは、GetPrinterDataEx 呼び出しを使用して、サーバーから構成データをダウンロードします。 構成データには、一般的なプリンターの説明 (GPD) ファイル、PostScript プリンターの説明 (PPD) ファイル、ドライバーのプロパティ バッグ、JavaScript の制約、リソース DLL などのデータ ファイルが含まれています。 クライアントでは、サーバーのドライバーに関連付けられていた CAT ファイルもダウンロードします。

印刷システムは、クライアントを検査し、リソース DLL に実行可能コードが含まれていないことを検証します。 印刷システムでは、ダウンロードしたファイルが有効であり、符号付きであるサーバーからダウンロードした CAT ファイルも検証します。 信頼されていないすべてのファイルは削除されます。 次の図は、Windows 8 クライアントと v4 プリンター ドライバーを使用する共有のプリント サーバーの間でこの構成に関連の通信を示します。

![構成に関連する windows 8 の印刷クライアントと v4 印刷ドライバーをプリント サーバーの間の通信。 getprinterdataex 呼び出しを使用して、構成情報がダウンロードされます。](images/win8and-epp.png)

## <a name="windows-7-and-windows-vista-client-connection-behavior"></a>Windows 7 および Windows Vista クライアントの接続動作


Windows 7 および Windows Vista のクライアントは、v4 プリンター ドライバーを使用する印刷キューの共有に接続も可能性があります。 ここでは、ただし、クライアントは常に拡張ポイント アンド プリント ドライバー サーバーからダウンロードします。 このドライバーでは、サーバー側のレンダリングを使用して、プリンターの適切なプリンターの記述言語 (PDL) が生成されることを確認します。

構成データは、GetPrinterDataEx 呼び出しを使用して Windows 7 および Windows Vista のクライアント接続に対して同じ方法で、サーバーからダウンロードされます。 ダウンロードしたファイルには、サーバーの CAT ファイルに対して検証が失敗した場合、削除されます。 次の図は、Windows 7 または Windows Vista クライアントと v4 プリンター ドライバーを使用する共有のプリント サーバーの間でこの構成に関連の通信を示します。

![windows 7 または windows vista 印刷クライアントと v4 印刷ドライバーをプリント サーバーの間の構成に関連する通信します。 getprinterdataex 呼び出しを使用して、構成情報がダウンロードされます。](images/win7and-epp.png)

V3 プリンター ドライバーによって提供される共有プリンターは、ポイント アンド プリントの既存のシステムを使用して作業を続けます。

## <a name="related-topics"></a>関連トピック
[V4 プリンター ドライバーの開発に関するベスト プラクティス](v4-printer-driver-development-best-practices.md)  



