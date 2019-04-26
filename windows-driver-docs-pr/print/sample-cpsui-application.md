---
title: サンプル CPSUI アプリケーション
description: サンプル CPSUI アプリケーション
ms.assetid: 895afbfe-c18a-4bcc-b815-8cb323bbac80
keywords:
- 共通のプロパティ シートのユーザー インターフェイスの WDK、印刷サンプル
- CPSUI WDK の印刷、サンプル
- WDK プロパティ シートのページを印刷するサンプル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8947ca126ea84b915b41e064e75239b6f8a40ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358724"
---
# <a name="sample-cpsui-application"></a>サンプル CPSUI アプリケーション





CPSUISAM、サンプル CPSUI アプリケーションでは、ソース コードが含まれている、 \\src\\WDK のディレクトリを印刷します。 アプリケーションは、CPSUI を呼び出すために、印刷スプーラー システムの既定のプリンターのプロパティ シートのページを作成します。 その後、アプリケーションでは、CPSUI を使用して、新しいページを作成するために使用できる手法の一部を説明するために、追加のプロパティ シート ページを作成します。

**注**  プリンター インターフェイス Dll は、印刷スプーラーに呼び出さないでください。 CPSUISAM は、CPSUI の機能の一部を示していますが、プリンター インターフェイス Dll によって使用される手法は表しません。 これらの Dll が記載された手順に従う必要があります代わりに、[プリンター ドライバーを使用して CPSUI](using-cpsui-with-printer-drivers.md)します。

 

 

 




