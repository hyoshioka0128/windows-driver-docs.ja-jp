---
title: デバイス固有のコンテキスト
description: デバイス固有のコンテキスト
ms.assetid: 29e0d451-57fb-4943-9508-022adffa4650
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9db03bb3969cd2ca9e761955e51dfe75242ba96c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840855"
---
# <a name="device-specific-contexts"></a>デバイス固有のコンテキスト





ミニドライバーは、必要に応じて、デバイス固有の情報を格納するためにプライベートコンテキストを使用することができます。 このデバイス固有のコンテキストによって、デバイス情報を取得するためにミニドライバーがデバイスを呼び出す必要がある回数を減らすことができます。 特定のミニドライバーのドライバー項目ごとに、デバイス固有のコンテキストを1つだけ指定できます。 ドライバー項目が不要になった場合、WIA サービスはミニドライバーの[**IWiaMiniDrv::D rvfreedrvitemcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext)メソッドを呼び出して、デバイス固有のコンテキストにアタッチされているすべてのリソースを解放します。

たとえば、カメラドライバーがデバイスからサムネイルデータを取得する場合、通常は、適切なドライバー項目に関連付けられているドライバーコンテキストのデータをキャッシュします。 WIA サービスによってコンテキストが解放されることに注意してください。 ドライバーの責任は、コンテキストによって保持されているすべてのリソースを解放するだけです。 前の例のサムネイルデータがデバイス固有のコンテキストで割り当てられたメモリに格納されていた場合、そのキャッシュされたデータを保持しているメモリはここで解放する必要がありますが、コンテキスト自体は解放しないでください。

 

 




