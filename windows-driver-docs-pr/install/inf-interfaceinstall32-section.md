---
title: INF InterfaceInstall32 セクション
description: このセクションでは、1 つまたは複数の新しいデバイス インターフェイス クラスを作成します。
ms.assetid: 7cd576a7-aa5b-486c-a622-cdcb9e7448b5
keywords:
- INF InterfaceInstall32 セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF InterfaceInstall32 Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bfef471012a1dd3d67c6318995a3ced70d0b035
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569775"
---
# <a name="inf-interfaceinstall32-section"></a>INF InterfaceInstall32 セクション


このセクションでは 1 つまたは複数を新規作成[デバイス インターフェイス クラス](device-interface-classes.md)します。 使用して、新しいデバイスのインターフェイス クラスをサポートするために、その後にインストールされているデバイスとドライバーを登録できる新しいクラスが作成されると、 [ **INF *DDInstall*します。インターフェイスのセクションでは**](inf-ddinstall-interfaces-section.md) 、それぞれの INF ファイル、または呼び出すことによって[ **IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506)します。

```ini
[InterfaceInstall32]
 
{InterfaceClassGUID}=install-interface-section[,flags]
...
```

## <a name="entries"></a>エントリ


<a href="" id="interfaceclassguid"></a>*InterfaceClassGUID*  
新しくエクスポートを識別する GUID 値を示す[デバイス インターフェイス クラス](device-interface-classes.md)します。

インターフェイス クラスのインスタンスを登録するには、このセクションで指定された GUID 値で参照する必要が、 [ **INF AddInterface ディレクティブ**](inf-addinterface-directive.md)で、 [ **INF *DDInstall*します。インターフェイス セクション**](inf-ddinstall-interfaces-section.md)、それ以外の場合、新しくインストールしたデバイスのドライバーを呼び出す必要がありますまたは[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)この GUID を持つ。

GUID を作成する方法の詳細については、[ドライバーを使用して Guid](https://msdn.microsoft.com/library/windows/hardware/ff565392)を参照してください。 システム定義のインターフェイス クラスの GUID など、適切なヘッダーを参照してください*Ks.h*カーネル ストリーミング インターフェイス。

<a href="" id="install-interface-section"></a>*インストール-section インターフェイス*  
場合によってはシステム定義された拡張機能の他の場所でこの INF のいずれかでの INF ライター定義のセクションを参照します。

<a href="" id="flags"></a>*フラグ*  
指定すると、このエントリがゼロにあります。

<a name="remarks"></a>コメント
-------

指定したときに*InterfaceClassGUID*が既にインストールされていないシステムでは、対応するインターフェイスのクラスがインストールされている<em>DDInstall</em>**します。インターフェイス**セクションは、によって処理される、 [SetupAPI](setupapi.md)デバイスのインストールまたはときにそのデバイスのドライバーは、最初の呼び出し中に関数**IoRegisterDeviceInterface**.

各*インストール-section インターフェイス*名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)を参照してください。

指定した任意*インストール-section インターフェイス*は次の一般的な形式があります。

```ini
[interface-install-section] | 
[interface-install-section.nt] | 
[interface-install-section.ntx86] | 
[interface-install-section.ntia64] | (Windows XP and later versions of Windows)
[interface-install-section.ntamd64] (Windows XP and later versions of Windows)
[interface-install-section.ntarm] (Windows 8 and later versions of Windows)
[interface-install-section.ntarm64] (Windows 10 and later versions of Windows)


 
AddReg=add-registry-section[, add-registry-section] ...
[AddProperty=add-property-section[, add-property-section] ...]  (Windows Vista and later versions of Windows)
[Copyfiles=@filename | file-list-section[, file-list-section] ...]
[DelReg=del-registry-section[, del-registry-section] ...]
[DelProperty=del-property-section[, del-property-section] ...]  (Windows Vista and later versions of Windows)
[BitReg=bit-registry-section[,bit-registry-section]...]
[Delfiles=file-list section[, file-list-section] ...]
[Renfiles=file-list-section[, file-list-section] ...]
[UpdateInis=update-ini-section[,update-ini-section]...]
[UpdateIniFields=update-inifields-section[,update-inifields-section]...]
[Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...]
...
```

内のエントリの詳細については、*インターフェイス-section インストール*を参照してください[ **INF DDInstall セクション**](inf-ddinstall-section.md)します。

設定できます以降 Windows Vista では、[デバイス インターフェイス クラス](device-interface-classes.md)プロパティを含めることによって[ **INF AddProperty ディレクティブ**](inf-addproperty-directive.md)インターフェイス インストール セクションでします。 含めることによって、デバイス インターフェイス クラスのプロパティを削除することも[ **INF DelProperty ディレクティブ**](inf-delproperty-directive.md)インターフェイス インストール セクションでします。 ただし、使用する必要があります、 **AddProperty**または**DelProperty**ディレクティブは、Windows Vista またはそれ以降のバージョンの Windows オペレーティング システムを新しいデバイス インターフェイスのクラスのプロパティを変更するだけです。 デバイス インターフェイス クラス、プロパティの Windows Server 2003、Windows XP、または Windows 2000 で導入された、対応するレジストリ値のエントリがある、使用する続行する必要があります[ **INF AddReg ディレクティブ**](inf-addreg-directive.md)と[ **INF してディレクティブ**](inf-delreg-directive.md)を設定し、デバイス インターフェイス クラスのプロパティを削除します。 システム定義プロパティとカスタム プロパティに次のガイドラインが適用されます。 使用する方法についての詳細、 **AddProperty**ディレクティブと**DelProperty**ディレクティブを参照してください[INF AddProperty ディレクティブとINFDelPropertyディレクティブを使用して](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md).

**AddReg**ディレクティブは、このインターフェイスのインストール中にレジストリにデバイスにインターフェイス固有の情報を設定する 1 つまたは複数のレジストリを追加セクションを参照します。 **HKR**などで指定された追加レジストリ セクションを指定、 **.DeviceClasses\\{**<em>InterfaceClassGUID</em>**}** キー。

レジストリのこのインターフェイスのクラスについては、少なくともの新しいフレンドリ名を含める必要があります[デバイス インターフェイス クラス](device-interface-classes.md)し、すべての情報を開き、このインターフェイスを使用しているときより高いレベルのコンポーネントに必要があります。

さらに、このような*インストール-section インターフェイス*ここで示すように、インターフェイスに固有のインストールの操作を指定する省略可能なディレクティブのいずれかを使用する可能性があります。

詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、 **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

## <a name="see-also"></a>関連項目


[**AddProperty**](inf-addproperty-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelProperty**](inf-delproperty-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506)

[**RenFiles**](inf-renfiles-directive.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

 

 






