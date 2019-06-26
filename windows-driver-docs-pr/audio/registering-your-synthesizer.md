---
title: ご利用のシンセサイザーの登録
description: ご利用のシンセサイザーの登録
ms.assetid: c8cb30ba-97ca-49ee-a6ef-2938a0ab780e
keywords:
- DirectMusic カスタム レンダリング WDK のオーディオ、シンセサイザー
- ユーザー モードの WDK オーディオ、シンセサイザーでカスタムの表示
- シンセサイザー WDK オーディオ、登録します。
- シンセサイザーの登録
- ユーザー モード シンセサイザー WDK オーディオ、シンセサイザー登録
- カスタムのシンセサイザー WDK のオーディオ、シンセサイザーの登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e6035a67c5be95d35f635b9d6547317a15c4f02
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362520"
---
# <a name="registering-your-synthesizer"></a>ご利用のシンセサイザーの登録


## <span id="registering_your_synthesizer"></span><span id="REGISTERING_YOUR_SYNTHESIZER"></span>


シンセサイザー、ソフトウェアを作成すると、後に列挙できる DirectMusic ポートとしてそれをアプリケーションに使用できるようにシステム レジストリに追加する必要があります。 インストール プログラムが DLL を呼び出すときに[ **DllRegisterServer** ](https://docs.microsoft.com/windows/desktop/api/olectl/nf-olectl-dllregisterserver)自体として COM に登録する DLL を指示する COM 関数オブジェクト、関数もシンセサイザーを登録できます。 これを行うには、関数は、次のパスにキーを作成して、利用可能なソフトウェアのシンセサイザーの一覧にエントリを追加します。

```inf
  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DirectMusic\SoftwareSynths
```

ヘッダー ファイル dmusicc.hdefines 定数 REGSTR\_パス\_SOFTWARESYNTHS をこのパスを表します。

シンセサイザーの COM オブジェクトのクラス識別子を持つキーと呼びます。 キー内では、文字列フィールドと呼ばれるシンセサイザーの名前の"Description"。

次のコード例は、関数の場合を示しています。 `RegisterSynth`、からに呼び出すことが**DllRegisterServer**シンセサイザーを登録します。

```cpp
  const char cszSynthRegRoot[] = REGSTR_PATH_SOFTWARESYNTHS "\\";
  const char cszDescriptionKey[] = "Description";
  const int CLSID_STRING_SIZE = 39;
  HRESULT CLSIDToStr(const CLSID &clsid, char *szStr, int cbStr);
 
  HRESULT RegisterSynth(REFGUID guid,
                        const char szDescription[])
  {
      HKEY hk;
      char szCLSID[CLSID_STRING_SIZE];
      char szRegKey[256];
 
      HRESULT hr = CLSIDToStr(guid, szCLSID, sizeof(szCLSID));
      if (!SUCCEEDED(hr))
      {
          return hr;
      }
 
      strcpy(szRegKey, cszSynthRegRoot);
      strcat(szRegKey, szCLSID);
 
      if (RegCreateKey(HKEY_LOCAL_MACHINE,
                       szRegKey,
                       &hk))
      {
          return E_FAIL;
      }
 
      hr = S_OK;
      if (RegSetValueEx(hk,
                        cszDescriptionKey,
                        0L,
                        REG_SZ,
                        (const unsigned char *)szDescription,
                        strlen(szDescription) + 1))
      {
          hr = E_FAIL;
      }
 
      RegCloseKey(hk);
      return hr;
  }
```

`CLSIDToStr` ローカルで定義されている CLSID 値を文字列に変換する関数 (上記のコード例では表示されません)。 似ています、 [ **StringFromCLSID** ](https://docs.microsoft.com/windows/desktop/api/combaseapi/nf-combaseapi-stringfromclsid) Microsoft Windows SDK ドキュメントで説明されている関数。

 

 




