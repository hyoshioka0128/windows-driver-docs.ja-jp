---
title: SetupAPI の使用に関するガイドライン
description: SetupAPI の使用に関するガイドライン
ms.assetid: a5005a4e-206a-4971-b89d-0d8f833d38c8
keywords:
- SetupAPI 関数 WDK、ガイドライン
- デバイスのインストールは、WDK SetupAPI を関数します。
- 一般的なセットアップは、WDK SetupAPI を関数します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a6abc3b0fe5f41edd2dae26ee97c5d92bb843b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374562"
---
# <a name="guidelines-for-using-setupapi"></a>SetupAPI の使用に関するガイドライン





使用するためのガイドラインを次に、[一般的なセットアップ関数](https://msdn.microsoft.com/library/windows/hardware/ff544985)(**セットアップ * **Xxx*) と[デバイスのインストール機能](https://msdn.microsoft.com/library/windows/hardware/ff541299)(** SetupDi***Xxx*) SetupAPI が用意されています。

-   ォヌーォソェホ インストール ファイルの内容は、エラーのない、または指定したインストール ファイルがされていない悪意を持って変更します。 そのため、常に SetupAPI 関数から受信したすべての情報を検証します。 文字列は、有効な長さ、有効なサイズのバッファーであることと、インデックス値が有効な範囲内にあることを確認します。

-   Microsoft Windows XP およびそれ以降のシステムでのインストール用のインストール アプリケーションを記述する場合は、呼び出す**SetupVerifyInfFile** (Windows SDK のドキュメントで説明)、ことを確認するデジタル署名された INF ファイル変更されていません。

-   常に各 SetupAPI 関数の戻り値をテストします。 関数が失敗した場合、コードを呼び出す必要があります[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)障害を識別するエラー コードを取得します。 返されたエラー コードを定義できる*Winerror.h*または*Setupapi.h*します。 呼び出しの前に**FormatMessage**でテキストの表示を作成する FORMAT_MESSAGE_FROM_SYSTEM、HRESULT_FROM_SETUPAPI マクロを使用して常に (で定義されている*Winerror.h*) への戻り値に変換する、HRESULT 値。 コードを呼び出してはならない SetupAPI 関数が正常に返された場合[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)します。 (、 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)と**FormatMessage**関数と、システムのエラー コードが、Windows SDK のドキュメントに記載されています)。

-   SetupAPI 関数がハンドルを返す場合 INVALID_HANDLE_VALUE の戻り値のコードを確認する必要があります。 このような関数が返されない**NULL**します。

-   次の違いに注意してください、**SetupDi * * * Xxx*と **セットアップ * * * Xxx*バッファーに必要なサイズのクエリを呼び出し元を許可する関数。

    -   場合の呼び出し元を **SetupDi * * * Xxx*関数は、このようなクエリでは、 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) ERROR_INSUFFICIENT_BUFFER は常に返します。

    -   場合の呼び出し元を **セットアップ * * * Xxx*関数は、このようなクエリでは、 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)バッファー長が指定されていないか、バッファーの場合、ERROR_INSUFFICIENT_BUFFER を指定する場合は NO_ERROR が小さすぎるを返します。

 

 





