---
title: WPP_CHECK_FOR_NULL_STRING を呼び出す必要があります。
description: WPP_CHECK_FOR_NULL_STRING を呼び出す必要があります。
ms.assetid: 4a4dfe91-a70b-4297-9f11-fcc4b0e5a900
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1763ff1609b98b888a0f55d8ab6651282507d77d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341659"
---
# <a name="do-i-need-to-call-wppcheckfornullstring"></a>WPP を呼び出す必要がある\_確認\_の\_NULL\_文字列でしょうか。


以降、Windows 7 バージョンの Windows Driver Kit (WDK) では、トレースのコンポーネントを自動的にチェック**NULL**トレース関数に渡す引数の文字列。 結果として、WPP を呼び出す必要はありません\_確認\_の\_NULL\_を防ぐための各引数の検証のため文字列**NULL**文字列から例外が発生します。

ビルドする場合、[トレース プロバイダー](trace-provider.md) (ドライバーやアプリケーションの場合) など、WPP を削除する Windows 7 以降のバージョンの WDK と\_確認\_の\_NULL\_文字列マクロソース コード。

 

 





