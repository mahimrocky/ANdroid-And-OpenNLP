#  Android and Open NLP

So here i will discuss how we can use Name entity recognization (NER) in android. For using NER we can use different type of NLP. But here we will use OpenNLP. 
**OpenNLP** Has many feature like tokenizer, sentence finder, person name finder, Organization or part of speech etc.
**OpenNLP** is java base library so we can use it android easily. So below section i will discuss how we will use it.

1. You have to download [**OpenNLP tools**](https://jar-download.com/artifacts/org.apache.opennlp/opennlp-tools/1.6.0/source-code) 
2. Copy the jar file and paste your android lib folder
3. Press rightclik on the jar file and hit **Add as a library**

Now you can use OpenNLP all class.
**So how to use Name entity recognization by OpenNLP??**

For this we have to download some file taht contains different rule and data to find data among texts.
First i will talk about how we can find person name among text. And remeber other things will be same like name finder. 
**N.B OpenNLP give you multiple possible Name.**
SO you have to use trick to choose the perfect name or whole name. It depends on work purpose.

SO now [**Goto this site**](http://opennlp.sourceforge.net/models-1.5/). Here you will get multiple language file. Now download **en-ner-person.bin** and **	en-token.bin** file. 
**N.B Downloaded file may be jar. SO don`t extract it just rename .bin**

1. Copy the bin files and paste it in your assets folder
2. Now we have to open name bin file and token bin file by code. By following code we can open it and use it.

Declare variables 
```sh
private Tokenizer tokenizer;
private NameFinderME nameFinderME;
public String Tokens[];
```
For open section. Befor read or find name we have to call below this method
```sh
public void openTokenzition() {
        InputStream is;
        TokenizerModel tm;

        try {
            is = getAssets().open("en-token.bin");
            tm = new TokenizerModel(is);
            tokenizer = new TokenizerME(tm);

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public void openNameFinder() {
        InputStream is;
        TokenNameFinderModel tokenNameFinderModel;

        try {
            is = getAssets().open("en-ner-person.bin");
            tokenNameFinderModel = new TokenNameFinderModel(is);
            nameFinderME = new NameFinderME(tokenNameFinderModel);
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
```

**Important section**
Suppos you have text or String. pass this string to below method.

```sh
 public void readToken(String tokens) {
        Tokens = tokenizer.tokenize(tokens);
    }
```
Yeah we parse and got the token.

Now you can find the possible names with multiline. You can try with multiple string or multiple line. I said it depends on work purpose.

For finding name:

```sh
public String readName(String cnt[]) {
        String sd = "";
        Span sp[] = nameFinderME.find(cnt);


        String a[] = Span.spansToStrings(sp, cnt);
        StringBuilder fd = new StringBuilder();
        int l = a.length;

        for (int j = 0; j < l; j++) {
            fd = fd.append(a[j] + "\n");

        }
        sd = fd.toString();
        return sd;
    }
```

For finding other things like organization or Part of speech you have to do same things like above.

# Happy coding
