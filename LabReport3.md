# **Lab Report 3 - Bugs and Commands**   
In this lab report, I reflect on my learning debugging and testing using JUnit and using various commands to get all kinds of information on repositories.   

---   

## Bugs:   
Here I demonstrate my process of debugging a program   

### Failure-Inducing Input:   
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
  @Test
  public void testReverseInPlaceLen3() {
    int[] input1 = { 0, 1, 2 };
    assertArrayEquals(new int[]{ 2, 1, 0}, ArrayExamples.reversed(input1));
  }
}

```
### Non-Failure-Inducing Input:   
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
  @Test 
  public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
  }
}
``` 
### Symptom:
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/25cd6c08-ea1d-4888-9ffb-3bf9dd5e7ea3)   
### Debugging:   
Before:   
```
public class ArrayExamples {
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
}
```
After:   
```
public class ArrayExamples {
  static void reverseInPlace(int[] arr) {
    int length = arr.length;
    for(int i = 0; i < length / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[length - i - 1];
        arr[length - i - 1] = temp;
    }
  }
}
```
### Explanation:   
The original code modifies the array while it is also being accessed, causing it to reverse elements already reversed. The fix I implemented creates a shallow copy of the parameter array which the new returned array can access to reverse its elements.   

---

## Researching Commands:   

##less   

The ```less``` command is used to view files in the terminal.   

---

### -N
```less -N <<file-name>>``` can be used to display line numbers beside the lines of a file.   
#### Examples:   
Input: ```less -N ./technical/biomed/1468-6708-3-1.txt ```   
Output:   
```
      1
      2
      3
      4
      5         Introduction
      6         Older adults are frequently counseled to lose weight,
      7         even though there is little evidence that overweight is
      8         associated with increased mortality in those over age 65.
      9         Six large controlled population-based studies of
     10         non-smoking older adults have investigated the association
     11         between body mass index (BMI) and mortality, controlling
     12         for relevant covariates [ 1 2 3 4 5 6 ] . All studies found
     13         excess risk for persons with very low BMI, but that persons
     14         with moderately high BMI had little or no extra risk except
     15         in certain small subsets. A review of 13 studies of older
     16         adults drew similar conclusions [ 7 ] .
     17         Many healthy older adults report gradual weight gain
     18         throughout adult life. It may be that a small amount of
     19         gradual weight gain is normative and associated with the
     20         most robust health as we age. It has been suggested that
     21         weight standards be adjusted upwards for age [ 8 ] . Such
     22         recommendations remain controversial, however, because the
     23         number of studies of older persons is fairly small, and
     24         because few studies have examined the relation of BMI to
     25         quality of life or years of healthy life (YHL) in the
```
Explanation: The column of line numbers does not traditionally show up. This command makes it easier to count and locate lines such as when fixing typos.   



Input: ```less -N ./technical/plos/journal.pbio.0020001.txt ```   
Output:
```
      1
      2
      3
      4
      5
      6         Kofi Annan, the Secretary-General of the United Nations, recently called attention to
      7         the clear inequalities in science between developing and developed countries and to the
      8         challenges of building bridges across these gaps that should bring the United Nations and
      9         the world scientific community closer to each other (Annan 2003). Mr. Annan stressed the
     10         importance of reducing the inequalities in science between developed and developing
     11         countries, asserting that “This unbalanced distribution of scientific activity generates
     12         serious problems not only for the scientific community in the developing countries, but for
     13         development itself.” Indeed, Mr. Annan's sentiments have also been echoed recently by
     14         several scientists, who present overwhelming evidence for the disparity in scientific
     15         output between the developing and already developed countries (Gibbs 1995; May 1997;
     16         Goldemberg 1998; Riddoch 2000). For example, recent United Nations Educational, Scientific,
     17         and Cultural Organization (UNESCO) estimates (UNESCO 2001) indicate that, in 1997, the
     18         developed countries accounted for some 84% of the global investment in scientific research
     19         and development, had approximately 72% of the world researchers, and produced approximately
     20         88% of all scientific and technical publications registered by the Science Citation Index
     21         (SCI). North America and Europe clearly dominate the number of scientific publications
     22         produced annually, with 36.6% and 37.5%, respectively, worldwide (UNESCO 2001).
     23
     24
     25             North America and Europe clearly dominate the number of scientific
```
Explanation: The column of line numbers does not traditionally show up. You can see more lines by pressing the down-arrow key. This command makes it easier to count and locate lines such as when fixing typos.   

Source: https://man7.org/linux/man-pages/man1/less.1.html

---
### -S   
```less -S <<file-name>>``` Truncates long lines rather than having the extra text wrap to the next line in the terminal. The truncated text can be seen by pressing the right-arrow key.   
#### Examples:   

Input: ```less -S ./technical/911report/chapter-1.txt```   
Output:
```
"WE HAVE SOME PLANES"

    Tuesday, September 11, 2001, dawned temperate and nearly cloudless in the eastern United States. Millions of men and women readied themselves for work. Some made their way to the Twin Towers, the signature structures of >

    For those heading to an airport, weather conditions could not have been better for a safe and pleasant journey. Among the travelers were Mohamed Atta and Abdul Aziz al Omari, who arrived at the airport in Portland, Maine.

INSIDE THE FOUR FLIGHTS

Boarding the Flights

    Boston: American 11 and United 175. Atta and Omari boarded a 6:00 A.M. flight from Portland to Boston's Logan International Airport.

    When he checked in for his flight to Boston, Atta was selected by a computerized prescreening system known as CAPPS (Computer Assisted Passenger Prescreening System), created to identify passengers who should be subject >

    Atta and Omari arrived in Boston at 6:45. Seven minutes later, Atta apparently took a call from Marwan al Shehhi, a longtime colleague who was at another terminal at Logan Airport. They spoke for three minutes.

    It would be their final conversation.

    Between 6:45 and 7:40, Atta and Omari, along with Satam al Suqami, Wail al Shehri, and Waleed al Shehri, checked in and boarded American Airlines Flight 11, bound for Los Angeles. The flight was scheduled to depart at 7:>

    In another Logan terminal, Shehhi, joined by Fayez Banihammad, Mohand al Shehri, Ahmed al Ghamdi, and Hamza al Ghamdi, checked in for United Airlines Flight 175, also bound for Los Angeles. A couple of Shehhi's colleague>
```
Explanation: The lines in this file are too long for the terminal to display each line without text wrapping. Using this command allows us to see the file line-by-line exactly as it is without modification.

Input: ```less -S ./technical/911report/chapter-1.txt```   
Output: ```./technical/plos/ is a directory```
Explanation: The less command cannot be used on directories as they can't be read and don't have lines like files.

Source: https://man7.org/linux/man-pages/man1/less.1.html

---   
### +n   
```less +n <<file-name>>``` Displays the file starting at line n.
#### Examples:   

Input: ```less +143 ./technical/plos/journal.pbio.0020001.txt```   
Output:
```
 United States contributed somewhat more publications to the top 10 journals (84%) than the
        top 11–20 journals (79%). The difference in the proportion of publications contributed by
        the United States to the top 10 and top 20 journals was even more pronounced when we
        examined it in respect to worldwide publications. In this case, the United States
        contributed 60% of the publications to the top 10 journals and only 40% of the publications
        to the top 11–20 journals.
        Interestingly, the proportion of publications from Latin America, the United States, and
        Canada across all subject areas in
        Science and
        Nature were nearly identical to those of the top 20 ecological journals.
        In
        Science and
        Nature , Latin America had 7% of the publications within the Americas
        versus 6% in the top 20 ecological journals, whereas the United States and Canada had 81%
        versus 82% and 12% versus 13%, respectively. These similarities suggest that the Latin
        American researchers are not shying away from the two top-ranked general science journals.
        However, publishing in
        Science and
        Nature was not enough to gain prominence, as evidenced by the number of
        citations of these researchers. The latest list of the 247 most-cited researchers in
        ecology and environmental sciences emphasizes the overwhelming contributions of authors
        from North America (73%) and Europe (21%) (ISI 2001b). No researcher working in a Latin
        American institution was included in the remaining 6%. Overall, these data indicate that
        the scientific output in the field of ecology in Latin America is having a relatively low
        impact in the international scientific community and is underrepresented in the top
```
Explanation: The output starts from line 143. This is useful if we want to see a specific section of a file and don't want to "scroll" all the way down there manually.   

Input: ```less +52 ./technical/911report/chapter-1.txt```   
Output:   
```
    At 7:50, Majed Moqed and Khalid al Mihdhar boarded the flight and were seated in 12A and 12B in coach. Hani Hanjour, assigned to seat 1B (first class), soon followed. The Hazmi brothers, sitting in 5E and 5F, joined Hanjour in the first-class cabin.

    Newark: United 93. Between 7:03 and 7:39, Saeed al Ghamdi, Ahmed al Nami, Ahmad al Haznawi, and Ziad Jarrah checked in at the United Airlines ticket counter for Flight 93, going to Los Angeles. Two checked bags; two did not. Haznawi was selected by CAPPS. His checked bag was screened for explosives and then loaded on the plane.

    The four men passed through the security checkpoint, owned by United Airlines and operated under contract by Argenbright Security. Like the checkpoints in Boston, it lacked closed-circuit television surveillance so there is no documentary evidence to indicate when the hijackers passed through the checkpoint, what alarms may have been triggered, or what security procedures were administered. The FAA interviewed the screeners later; none recalled anything unusual or suspicious.

    The four men boarded the plane between 7:39 and 7:48. All four had seats in the first-class cabin; their plane had no business-class section. Jarrah was in seat 1B, closest to the cockpit; Nami was in 3C, Ghamdi in 3D, and Haznawi in 6B.

    The 19 men were aboard four transcontinental flights.

    They were planning to hijack these planes and turn them into large guided missiles, loaded with up to 11,400 gallons of jet fuel. By 8:00 A.M. on the morning of Tuesday, September 11,2001, they had defeated all the security layers that America's civil aviation security system then had in place to prevent a hijacking. The Hijacking of American 11 American Airlines Flight 11 provided nonstop service from Boston to Los Angeles. On September 11, Captain John Ogonowski and First Officer Thomas McGuinness piloted the Boeing 767. It carried its full capacity of nine flight attendants. Eighty-one passengers boarded the flight with them (including the five terrorists).22 The plane took off at 7:59. Just before 8:14, it had climbed to 26,000 feet, not quite its initial assigned cruising altitude of 29,000 feet. All communications and flight profile data were normal. About this time the "Fasten Seatbelt" sign would usually have been turned off and the flight attendants would have begun preparing for cabin service.

    At that same time, American 11 had its last routine communication with the ground when it acknowledged navigational instructions from the FAA's air traffic control (ATC) center in Boston. Sixteen seconds after that transmission, ATC instructed the aircraft's pilots to climb to 35,000 feet. That message and all subsequent attempts to contact the flight were not acknowledged. From this and other evidence, we believe the hijacking began at 8:14 or shortly thereafter.
```
Explanation: The output starts from line 53. This is useful if we want to see a specific section of a file. 

Source: https://man7.org/linux/man-pages/man1/less.1.html

---   

### -p   
```less -p <<pattern>> <<file-name>>``` Displays the file starting at the first line containing the pattern.   
#### Examples:   

Input: ```less -p American ./technical/911report/chapter-1.txt```   
Output:
```
     Boston: American 11 and United 175. Atta and Omari boarded a 6:00 A.M. flight from Portland to Boston's Logan International Airport.

    When he checked in for his flight to Boston, Atta was selected by a computerized prescreening system known as CAPPS (Computer Assisted Passenger Prescreening System), created to identify passengers who should be subject to special security measures. Under security rules in place at the time, the only consequence of Atta's selection by CAPPS was that his checked bags were held off the plane until it was confirmed that he had boarded the aircraft. This did not hinder Atta's plans.

    Atta and Omari arrived in Boston at 6:45. Seven minutes later, Atta apparently took a call from Marwan al Shehhi, a longtime colleague who was at another terminal at Logan Airport. They spoke for three minutes.

    It would be their final conversation.

    Between 6:45 and 7:40, Atta and Omari, along with Satam al Suqami, Wail al Shehri, and Waleed al Shehri, checked in and boarded American Airlines Flight 11, bound for Los Angeles. The flight was scheduled to depart at 7:45.

    In another Logan terminal, Shehhi, joined by Fayez Banihammad, Mohand al Shehri, Ahmed al Ghamdi, and Hamza al Ghamdi, checked in for United Airlines Flight 175, also bound for Los Angeles. A couple of Shehhi's colleagues were obviously unused to travel; according to the United ticket agent, they had trouble understanding the standard security questions, and she had to go over them slowly until they gave the routine, reassuring answers.      

    Their flight was scheduled to depart at 8:00.

    The security checkpoints through which passengers, including Atta and his colleagues, gained access to the American 11 gate were operated by Globe Security under a contract with American Airlines. In a different terminal, the single checkpoint through which passengers for United 175 passed was controlled by United Airlines, which had contracted with Huntleigh USA to perform the screening.

    In passing through these checkpoints, each of the hijackers would have been screened by a walk-through metal detector calibrated to detect items with at least the metal content of a .22-caliber handgun. Anyone who might have set off that detector would have been screened with a hand wand-a procedure requiring the screener to identify the metal item or items that caused the alarm. In addition, an X-ray machine would have screened the hijackers' carry-on belongings. The screening was in place to identify and confiscate weapons and other items prohibited from being carried onto a commercial flight.
```
Explanation: The output starts from the first line with the pattern "American." The command can be used to find the first instances of any pattern. It also highlights other instances of the pattern making it a convenient search tool.

Input: ```less -p President ./technical/911report/chapter-2.txt```   
Output:   
```
                (such as those promoted by Egyptian President Gamal Abdel Nasser's Arab Socialism or
                the Ba'ath Party of Syria and Iraq) that called for a single, secular Arab state.
                However, what emerged were almost invariably autocratic regimes that were usually
                unwilling to tolerate any opposition-even in countries, such as Egypt, that had a
                parliamentary tradition. Over time, their policies- repression, rewards, emigration,
                and the displacement of popular anger onto scapegoats (generally foreign)-were
                shaped by the desire to cling to power.
            The bankruptcy of secular, autocratic nationalism was evident across the Muslim world
                by the late 1970s. At the same time, these regimes had closed off nearly all paths
                for peaceful opposition, forcing their critics to choose silence, exile, or violent
                opposition. Iran's 1979 revolution swept a Shia theocracy into power. Its success
                encouraged Sunni fundamentalists elsewhere. In the 1980s, awash in sudden oil
                wealth, Saudi Arabia competed with Shia Iran to promote its Sunni fundamentalist
                interpretation of Islam, Wahhabism. The Saudi government, always conscious of its
                duties as the custodian of Islam's holiest places, joined with wealthy Arabs from
                the Kingdom and other states bordering the Persian Gulf in donating money to build
                mosques and religious schools that could preach and teach their interpretation of
                Islamic doctrine. In this competition for legitimacy, secular regimes had no
                alternative to offer. Instead, in a number of cases their rulers sought to buy off
                local Islamist movements by ceding control of many social and educational issues.
                Emboldened rather than satisfied, the Islamists continued to push for power-a trend
                especially clear in Egypt. Confronted with a violent Islamist movement that killed
                President Anwar Sadat in 1981, the Egyptian government combined harsh repression of
                Islamic militants with harassment of moderate Islamic scholars and authors, driving
                many into exile. In Pakistan, a military regime sought to justify its seizure of
```
Explanation: The output starts from the first line containing the pattern "President". The command also highlights other instances of "President" allowing for easy searching of the pattern.

Source: https://man7.org/linux/man-pages/man1/less.1.html
