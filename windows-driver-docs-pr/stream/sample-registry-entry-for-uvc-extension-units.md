---
title: UVC 拡張ユニットのサンプル レジストリ エントリ
description: UVC 拡張ユニットのサンプル レジストリ エントリ
ms.assetid: a34e00e2-90f0-4073-8740-7f3e04d68639
keywords:
- レジストリ WDK USB ビデオ クラス
- 拡張機能ユニット WDK USB ビデオ クラス、サンプル、レジストリ エントリ
- サンプル コード UVC 拡張機能のユニットのレジストリ エントリの WDK USB ビデオ クラス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48044c0d53220ad3213b304352b19bb68f9ddb19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389209"
---
# <a name="sample-registry-entry-for-uvc-extension-units"></a>UVC 拡張ユニットのサンプル レジストリ エントリ

このトピックには、ユニットの拡張機能をサポートするために使用できるサンプル レジストリ エントリが含まれています。

エントリを追加する必要があります、 **HKLM\\システム\\CurrentControlSet\\コントロール\\NodeInterfaces**レジストリ サブキー。 このレジストリ サブキーには、プロパティ セット GUID の値とそのプロパティ セットに対応するインターフェイスの IID および CLSID の値が含まれています。

確認します。

- プロパティ セット GUID 一致の GUID、[拡張ユニット記述子](sample-extension-unit-descriptor.md)します。

- 内の IID および CLSID 値、 **NodeInterfaces**サブキーは、リトル エンディアン バイナリ形式で格納されます。

したがって、として、{12345678-1234-5678-0123456789abcdef} の値が IID が格納されます。

```cpp
78 56 34 12 34 12 78 56 01 23 45 67 89 ab cd ef
```

- Guid は一意である必要がありを使用して生成する必要があります*Guidgen.exe*、Microsoft Windows SDK に含まれているツールです。

次のコードを任意の名前、レジストリ スクリプトに含める*Xusample.rgs*:

```cpp
HKLM
{
    NoRemove SYSTEM
    {
        NoRemove CurrentControlSet
        {
            NoRemove Control
            {
                NoRemove NodeInterfaces
                {
                    ForceRemove {xxxxxxxx-xxxx-xxxx-xxxx-
                       xxxxxxxxxxxx} = s 'Extension Unit
                       Property Set'
                    {
                        val IID = b 'yyyyyyyyyyyyyyyyyyy
                           yyyyyyyyyyyyy'
                        val CLSID = b 'zzzzzzzzzzzzzzzzz
                           zzzzzzzzzzzzzzz'
                    }
                }
            }
        }
    }
}
```

プラグインの DLL を登録することでインストールをサポートするために、レジストリ スクリプトに次のコードを追加します。

```cpp
HKCR
{
    NoRemove CLSID
    {
         ForceRemove {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} = s 'CompanyName Extension Unit Interface'
        {
            InprocServer32 = s '%MODULE%'
                                                {
                                val ThreadingModel = s 'Both'
                                                }
        }

    }
}
```
