# DTBSUPLD

def CalcObligorRating(rating):
   
    ratingDF = pd.DataFrame(
                data=({"Moodys":['Aaa','Aa1','Aa2','Aa3','A1','A2','A3','Baa1','Baa2','Baa3','Ba1','Ba2','Ba3','B1','B2','B3','Caa1','Caa2','Caa3','Ca','C','D'],
                        "S&P"  :['AAA','AA+','AA' ,'AA-','A+','A' ,'A-','BBB+','BBB' ,'BBB-','BB+','BB' ,'BB-','B+','B' ,'B-','CCC+','CCC' ,'CCC-','CC','C','D'],
                        "Fitch":['AAA','AA+','AA' ,'AA-','A+','A' ,'A-','BBB+','BBB' ,'BBB-','BB+','BB' ,'BB-','B+','B' ,'B-','CCC+','CCC' ,'CCC-','CC','C','D']}))
    
    scoreList = [ratingDF[ratingDF.iloc[:,i] == rating[i]].index[0] if rating[i] in ratingDF.iloc[:,i].values else -1 for i in range(len(rating))]
    obligorRating = ratingDF['S&P'].iloc[max(scoreList)]
    return obligorRating


reportEnd = df[df.isna().all(axis=1)].index

df =df.drop(df.iloc[reportEnd:].index)





from datetime import datetime
def date_std(source, report_name):
    try:
        if source == "Barclays":
            report_date = report_name[:-5][-11:]
            date_obj = datetime.strptime(report_date, '%d %b %Y')

        elif source == "BMO":
            report_date = report_name[0:10]
            date_obj = datetime.strptime(report_date, '%Y.%m.%d')

        elif source == "Scotiabank":
            report_date = report_name[:-5][-8:]
            date_obj = datetime.strptime(report_date, '%d.%m.%y')

    except:
        raise Exception(source +" Report name has no valid date!")

    date_str = date_obj.strftime('%Y-%m-%d')
    return date_str

#print(date_std("Barclays", "abcde 16 Oct 2023.xlsx"))
#print(date_std("BMO", "2022.05.31 abcde.xlsx"))
print(date_std("Scotiabank", "3.3-1 07.10.23.xlsx"))
#print(date_std("BMO", "2022.05 abcde.xlsx"))


