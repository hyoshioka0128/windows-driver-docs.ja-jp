---
title: カスタムのデバイスのプロパティを作成します。
description: カスタムのデバイスのプロパティを作成します。
ms.assetid: e18fcbe8-6083-451e-b1be-5a543b61c627
keywords:
- デバイスのプロパティのカスタムの作成、WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ec294e7d9e6dacaa47fdb9e7d8de8664aa4d0fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557675"
---
# <a name="creating-custom-device-properties"></a>カスタムのデバイスのプロパティを作成します。


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)デバイスのインスタンスのプロパティのカスタム デバイス カテゴリの作成をサポート[デバイス セットアップ クラス](device-setup-classes.md)、デバイスクラス、およびデバイスのインターフェイスをインターフェイスします。 カスタム プロパティを呼び出して、適切なアクセスできる[SetupAPI プロパティ関数](https://msdn.microsoft.com/library/windows/hardware/ff541483)します。 使用して、カスタムのデバイス プロパティを変更こともできます、 [ **INF AddProperty ディレクティブ**](inf-addproperty-directive.md)または[ **INF DelProperty ディレクティブ**](inf-delproperty-directive.md)します。

カスタムのデバイス プロパティの詳細については、次のトピックを参照してください。

[カスタムのデバイス プロパティのカテゴリを作成します。](#creating-custom-device-property-categories)

[カスタムのデバイス プロパティにアクセスする SetupAPI プロパティ関数を使用します。](#using-the-setupapi-property-functions-to-access-custom-device-properti)

[INF AddProperty ディレクティブまたは INF DelProperty ディレクティブを使用して、カスタム デバイス プロパティを変更するには](#using-the-inf-addproperty-directive-or-the-inf-delproperty-directive-t)

### <a href="" id="creating-custom-device-property-categories"></a> カスタムのデバイス プロパティのカテゴリを作成します。

カスタムのデバイス プロパティのカテゴリは、論理的に関連するカスタム デバイスのプロパティのコレクションです。 プログラムによってカスタム デバイス プロパティのカテゴリを作成するには、使用、 [ **DEFINE_DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff541072)マクロを次のようにプロパティのカテゴリのプロパティを表すプロパティのキーを作成します。

-   プロパティのカテゴリを表す一意の GUID 値を作成し、各プロパティのキーの GUID 値をこの一意の GUID 値に設定します。 新しい GUID 値を作成する方法については、[の定義およびエクスポートする新しい Guid](https://msdn.microsoft.com/library/windows/hardware/ff542998)を参照してください。

    **注**  プロパティのシステム定義のカテゴリはオペレーティング システム専用として予約されています。

     

-   プロパティのカテゴリ内で一意であるし、2 つ以上ある整数値には、各プロパティのキーのプロパティの識別子を設定します。

使用して、デバイスのインスタンスのカスタム デバイス プロパティのカテゴリを作成することも、 [ **INF AddProperty ディレクティブ**](inf-addproperty-directive.md)します。

### <a href="" id="using-the-setupapi-property-functions-to-access-custom-device-properti"></a> カスタムのデバイス プロパティにアクセスする SetupAPI プロパティ関数を使用します。

」の説明に従って、カスタム デバイスのプロパティを同じ方法でアクセス[プロパティにアクセスするデバイス (Windows Vista 以降) を使用して SetupAPI](using-setupapi-to-access-device-properties--windows-vista-and-later-.md)します。 カスタムのデバイスのプロパティにアクセスするときに、次の追加の考慮事項が適用されます。

-   **SetupDiGetXxxPropertyKeys**と**SetupDiGetXxxPropertyKeysEx**関数は、デバイスのシステム定義プロパティのキーとはプロパティを表すカスタム デバイス プロパティのキーを取得コンポーネントを設定します。

-   **SetupDiSetXxxProperty**関数は、コンポーネントのカスタム デバイス プロパティを設定します。 Windows は、カスタムのデバイス プロパティのキー、プロパティのデータ型およびプロパティの値に内部的に関連付けます。 同じプロパティのキーを持つカスタムのデバイス プロパティが設定されて既に場合、 **SetupDiSetXxxProperty**関数は、プロパティの値と、プロパティに関連付けられているプロパティのデータ型が上書きされます。

-   **SetupDiGetXxxProperty**関数は、コンポーネントが設定されているカスタムのデバイス プロパティを取得します。 **SetupDiGetXxxProperty**関数は、プロパティの設定時に設定されたプロパティのデータ型とプロパティ値を取得します。

### <a href="" id="using-the-inf-addproperty-directive-or-the-inf-delproperty-directive-t"></a> INF AddProperty ディレクティブまたは INF DelProperty ディレクティブを使用して、カスタム デバイス プロパティを変更するには

使用してカスタムのデバイス プロパティを変更する、 [ **INF AddProperty ディレクティブ**](inf-addproperty-directive.md)コンポーネントをインストールしているセクションで、AddProperty ディレクティブを追加し、プロパティに次のエントリを指定:

-   *プロパティ カテゴリの guid*カスタム デバイス プロパティのカテゴリを表すエントリ

-   カスタムのデバイス プロパティのカテゴリ内でプロパティを識別するプロパティの識別子のエントリ

-   *値*新しいデバイス プロパティのエントリまたは*値*エントリ既存のデバイス プロパティの値を変更します。

使用して、 [ **INF DelProperty ディレクティブ**](inf-delproperty-directive.md)カスタム デバイス プロパティを削除します。

これらのディレクティブを使用する方法の詳細については、、 [INF AddProperty ディレクティブと INF DelProperty ディレクティブを使用して](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)を参照してください。

 

 





