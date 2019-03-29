---
title: 通知オブジェクト DLL およびクラス オブジェクトの読み込み
description: 通知オブジェクト DLL およびクラス オブジェクトの読み込み
ms.assetid: 846c0ed8-5299-4803-983a-9347e912d96b
keywords:
- オブジェクトの読み込み、オブジェクトの WDK ネットワークへの通知します。
- ネットワークがオブジェクトの読み込み、WDK をオブジェクトに通知します。
- 読み込みオブジェクト WDK オブジェクトに通知します。
- WDK の Dll オブジェクトに通知します。
- クラス オブジェクト WDK オブジェクトに通知します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aaa800978ff03f38d81704879b0b3b3a51e31c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580364"
---
# <a name="loading-the-notify-object-dll-and-class-object"></a>通知オブジェクト DLL およびクラス オブジェクトの読み込み





ネットワーク コンポーネントのオブジェクトは、コンポーネント オブジェクト モデル (COM) オブジェクトとして実装する必要がありますに通知します。 これらの COM オブジェクトは、COM コンポーネントのサーバー Dll 内に存在します。 DLL の COM サーバーの開発に関する詳細については、Microsoft Windows SDK を参照してください。

一連のエントリ ポイント関数をエクスポートする特定の通知オブジェクトの DLL を実装する必要があります。

-   A **DllMain**サブシステムの仮想アドレス空間に DLL を読み込むネットワーク構成のサブシステムを使用する関数。

-   **DllRegisterServer**と**DllUnregisterServer**クラス オブジェクトを dll のオペレーティング システムのレジストリに情報を格納する関数。 検索と読み込みのネットワーク コンポーネントには、このレジストリ情報が通知のネットワーク構成のサブシステムでは、次のオブジェクトです。

-   A **DllCanUnloadNow**ネットワーク構成サブシステムが、DLL が使用中かどうかを確認できるようにする関数。 DLL が使用されていない場合、サブシステムは安全にメモリから DLL をアンロードできます。

通知オブジェクトの DLL で COM サーバーにするには、クラス ファクトリを公開して、通知オブジェクトのサーバーをサポートしているある必要があります。 このクラスのファクトリは、通知オブジェクトのインスタンスを作成、ネットワーク構成のサブシステムを使用できます。 クラス ファクトリを継承する必要があります、 **IClassFactory**インターフェイス。 継承するクラスの実装の詳細については**IClassFactory**、Windows SDK を参照してください。

 

 





