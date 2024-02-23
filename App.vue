<template>
  <div class="pdf">
    <form ref="myForm">
      <!-- Your form fields go here -->
      <label for="name">Name:</label>
      <input type="text" id="name" v-model="formData.name" required />

      <label for="email">Designation</label>
      <input type="email" id="email" v-model="formData.name" required />

      <label for="num">Contact No</label>
      <input type="text" id="num" v-model="formData.name" required />

      <label for="dept">Department</label>
      <input type="email" id="dept" v-model="formData.name" required />

      <!-- Add more form fields as needed -->

      <button type="button" @click="downloadPDF">Download PDF</button>
    </form>
  </div>
</template>

<script>
import jsPDF from "jspdf";

export default {
  name: "pdfAbc",
  data() {
    return {
      formData: {
        name: "",
        email: "",
        // Add more fields as needed
      },

      imagePath: "back.jpg",
    };
  },
  methods: {
    downloadPDF() {
      const pdf = new jsPDF();
      const formData = this.formData;

      // Load the image from the local file system
      const imageData =
        "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMwAAADMCAMAAAAI/LzAAAABdFBMVEUAAAD///+WKwe8oom/pYuYmJjLysrDqI6VKACZLAeNAACUJQCTIQCcLQeIAAD5+fm4uLizmoKRFwCJFABXY2U5AADN0NDr6+vg4OCfn5/11t9xe3z28O/BwcHy8vKdhnGsrKx5eXmhKgCUfmqokHmBDACKiorplrSBgYHg1cuLKAd9aVhiYmJAQEAQAACLdmNVSDwgGhZsAADhy8hAEgM4LSbWuLPt4N5gUURRUFBsbGxnHgVBNi0SDgxZAAAfAACrz+F2QT60d21uXk+ZNBmtaFwqJB6jUkhEAADMpqLi7vQjIyM2MzPBkYmdQTJ5IwbSwbKXMS8tAACmWVmJvdXZMXbinJtlrMvbf3vYcW7swsFaGgSEbW0gEAubPz6XLyJ2KiJaLzJhMypFKy1nQj9pT0wAGx4tERVUIBjhbpkgNDaQFhfUG1zyxtTlhKjtscWatsPcToIqlr7lrq7QT03MOzrAAADIISCXiJ1KXIVka4w0EQnYIH/9AAAgAElEQVR4nO19iX/aZra2xCYQsl8Jt1oSIYTBKja7CQgIOBmwIcQGO+M0ax3P9DZz25vp9GuTuTP39p//znklsdvgJmlm7i9npjE776OzPee8CwzzWT7LZ/ksn+WzfJbP8lk+y7+XtMvVVqs0I61qr9z+1OO6qZRbpW63WEwk0pLfkUAA/pHSiVQx2+2WWuVPPcI1pVrPFlPpNBfgOC4AwjmCYJzbgUA6ncp2S71PPdIVclHPptJSwB07qiUgZVG69QTqB0D6/QiH4/ygpWyp8KlHfJX06gDEz6FBpYuAI1XNwl0JnrmA/7IALA1eVCrVswHH8AJgd/+aeEopybEjHGmpneL8RaaUhjvdYhaeTKDzJJgLdJYW5594kpQutj712Gfloig53pGol6SAnysxdS6QYFoIJgA38EG4VWS6nF9Kpf3TgorsfmoAE2klwAVgUKkS3CmDTrg6U+IC6V4hQTG4qPyBLNwA7QWmoVBdclzqXyIclOtpalpcEe4U2kWJ3m4zAKbFpCiGtAemxKCDtKa1UmxVu6gpUGrpU2egaldCJOguCfBspuxHf+BSCEaqM0X/DJhWoVVvtabA+FtMu0eDA4VT/5TqgYtKldLtJThqMWUmS51bKjNpzt91RjkBU+ilwCClMRSuy/SyiW7P0eAnhdPrJjgaiLke+DsdDfoKvdEDpaTrc2D88JbUhBRADmozgI7LMl03toHvfBpjq6fgu6ViYtrDU0yVxi245BfdFtNzAkD6ok6fTuPb2tXSWDFFpsqhUZbpQ/BZAEcqln53KK2iBGqBL8aoG6gWHPMKMOUiR695tsxclFLOoKWEE4ylVLHYrbcmYLpUkYCJPpRoUw/k0tnf19YK3TQ1iXKb0hRIIE4moQnGCVNpx54kFOdf+EuT5DjNgH1B/gz4XXNEjbSy+JrE76mcagqGINUhm1cTjsNfXDgaKTItyUsjMHg/d3Z2ZtsqiA23zjjnUQ9Mut0ucoFsuwBWiLaayLaZnhOxfzdaXXfGC3m/5FxT4CzwoGNJ+BwogTvbtQnrCtF17zYxds/OPERgZ+1qq00/hKuCUrl0nXIdINbV3wdLkXOva4BLMb20mxd7Cc5TCHdm03HbteFwdHh46ON5PgZ/D/vDQYU+xdoOIC4FWbRcBMsCxymgnj16EOB+D4pTljgkvBiR/ZgXu06QrbeLzjC4XcISUhkcbYLwMSEajYZR4G9U4Hl4MHZUo0rbRefnpDRH8yzT7sLwS2MjxSD3kaG0S3DtpGK3mHa/8MLhX6gP9BAbTKoy7COMsO8KCcf4Tb5Ts3WW7HL0slCDa/mB0RT9E+Gkj2tqvSx6apVpe2kOncX78rNdndiV4eV1QKYA8aMh2Jx+5lhnC62Xm+Kg8EWc/2Nm0CqaklTuZYvZtOSk+kSPoUoCh0ckIzCsVUBciYDR9QcVneyC//il7jSXRsMtAiHyZz+aqVXRooDHZ4FEZd160V+EolLiQCngJjy/LhJXBD4M9kbss4Cfm8ECV6kNlQXE6I9kag5lAevupigfdKNaQOIqOguOElttXYsSjglHQ5u1K1P5x9XMRTUFLpX6KGhcsghRuF1mWqliu+yAkc4ASme0tnktwon1Ec7ZHBpgE8CNAM1HIDfAIF2rTpWg3ge6f4FgJA7G8R5QUCKC8KoDuYebhsMVe0yv3QUKlPjgfnPhh6K+5eYSrHNLtJ7377Js55EQfQ8oHpwBS6aUw0HMLEo9zMmB9IcGA5kNiBf1k4AfCGIPOSJaWO1R7H2hUInG+hXWDrhwOKi5S+D/jpt+WDQXAaoOKO2p1xerbcr5d1n7iF8NJQIEYDUaSD1DnT1z3b/klnkutA+IpQyWiwSeAzKboiSE/t8mtUt+jVFu7f3pbjSyxgt5UA6SHKRJVZfYBKQ0DdQfCgsUjAGpelEHDgNJLOXGgTPWHq7KK4hg409fWObtu6ibyCpEMX6g62fgJa1q2sMC1Q4UoMUPhKaXCtCQUqhWW91qwW257LKV/gq1RKI7ACf8Z5Vl5T8A7I3TrY1Vytns2CyiSUywXFDbzn4QNO0sNh25FMTJYrbUugBGCHkSTCwcW4Fl60/Nb7c2tv8DwCjfwI2Xze/2V5qba2puQk6XoEBvMQnauPoA4pZikLzKRSjnU9lUAKKYPlwVxCJ7r001/uf9BxksYIIP9h9oSijzJ99KUzussbuBcUwD8pTulVMBxPXeQstg+tmgmyz2VgP+M8PubK0KUJFTC0DImqggGEXURPijNndWRgLhcKDTBAqJjWm1oGJLYx7AzPOe0ktzgWKLVpEBRENdn9id1TzMAcNOamf8R369tep9kHK2hrqB39gGs0j0ymmOtne4920MtMH3IOZjNxzRlAtY67L2+RqcMrL1jUpRqMEcSJDeEQ/WIaPhrY5OwAS62BYoMr2AYxrce7pNiWZ8sNau00NOUyyjlVg2tre3hT+EEMpx0sokkxkrU5ZZoh3AE9urYhpkHEAD162O5UZxMgXyXpzzwu1dQHVepTEtgFiEFWEMsDz4y38+eBAELM2GeWLJVkbW8sFGjlVzD75s/+XuSjQR/khnJdpSm5oC4dLvE5+9jgsHaabqXCBW76/E4otWWUWWWdbIWTn0ew1xiXBHMUJgbn/ZXvkJPr5DdAmyZ5lWhNg7lGjb8DdLfUyPsLmAneMA0VelSlTMgUm9xcgkG9TvtSD+IblmxsC7t/fXIDebQ3YXEk0W279SFiJZr0i7a79RetPlhVQvgWpscr4GG9vYz9DBa81kOT4BI+eaTQ1uqLnV8RksbXOAaGguqDPtVqnHpN6DcqamewyUju+SIR/ZCEc3Vgxm44DmmGRTNZm4B0Y9tuCREGDZX+EzkQ2QSHizxtIKB6JYtShJxV5Vwgj3m6TunxXAwg5iGzsHL18e7FwfziLb91SWiA3wF5MRHTBy3iKs2DBZ63TFtYhsHbw8ONjfCB9WEE0gwUCqAbJZZ+B6Sr9pbrqXnm3+QCnGVi63D16LoZD5zd1r0ESiW7E/yqwKMYx10EAACCEWfEz5Ymdn6zqKBjxIDMXFbx6Ehb4NHBono6jzlhj02tRvAZOdU4yf0+2+IOQddpI8vRpN9PvXr3OoCpO6O6AxNTkfxDtEzMuh3OvXD64xtPC3Io0e2sGG0NF3XTABnPCVnLrtxtKaV4x/V+/ENr4MOeRE/u5KMJF9SzFg5KG86LxWbDetvObwGjEfIoahJK8OAZFow6VAzHY4NoCCQGLKCU4KBLoph/HePNlk57pyUIzVYuENxmVa6snO1lXypROYQ/mkqWmaCf8oYGgmlWQ+jkPVvtzC9+/MCT6ytZN3v6Ox5YteVlggh0y7PWmp37wYAMWMUy/tMXGk4hN8YzCs+cWVQg2KZeP5k0ajkQeBlKnBn5OTk/yxAwaidrN5e4ngw6r7FRako9iRbdOZD2d+Ecdy8+kB5ETYtKKOV3KMDDLMBMxqkT0zU3MZMy+7JueAWUsyO+BZPBoaXdrlLLXpUpJzU8UgvSzSLka7RI0Ms+UNwRjOX8uygozjbGJDXvsDaO0TFcDQXAORcJFN98ZrU7DBVywVcFIZTBRSP7EvBQpGlkNripmzVAcLhmaNZk9Va2jrvFcOybL6xQ4GBP6I2BKFkgCN9EqYym+kGuyNBDgpCwmq1G3X/dIuO6Q0ZoMBdw6uKZlGHCMF5BckmhRNPJdZ6600cOSdQg6IAE7sFuttpnCR8nM3LdPc+W8uTQkepCpS4SO+G5oZG2painyCTIbSGWA2htWMr//+2ztO2rrUgT+ncKqrXMCLDEq6AQ0oJ8ZxLJ3tdVExLu+/CRiiBCG/UIrpEE2zbTW1td2fZXNurcEPIQYkStkE1FVZsJdUgLtB42myVA/5pYRhedN3UzBEjCvJ5MlUCcA2mjnNCQpryRcumDBPdFw5BcHsogymDylHWt/OitMJM4CKGQnrgSH6+FYmaakq1GMq6xZnSi6Yi5vJKUPTr1dT3uuXUtVQL64W2pBxbtQOCPi9Bbw0vHNGzSv6V4G59YN3y4DMbxHlJHO7KbOmxsrNZPBYNcykHB8H5x/05Z/iyn95nbnwG/AaqGVK5QJToA1VLrEulhIH7la46FVbIGCk4DHeNVoJ5q+3vJskaMZNCGRty2qcnDQy1nEQEZrm2M5+/Ov1YJhtj6/FUDXYbr5IcW5bYt1Ft2koK5lCuQzXgWkDFdArlx6r3LinXvv9P/7tK++moYasILAy1sxR0cDQtIxoyGPb+upvP64JJvpIt/1SqeVBWb8bUMBWWbtQTyXa7SwkzV32aNzs3/jj9WB+0P82vm2EZDGTVBVVce/LSUs2p0LzV7f+xl4nEzDhwwEB9sxxLlOEJCqtBwaLB6lbZrJFMDh4u22/moD58no28jd9ZnxaSDMz8aaqqkSVrTzoSp558Q/sdTIB4xPOyS4SRUgyUjrVLaXXbW04vZ1sj7nAMtV/Rga+8Jpgbv3040/T91UrTppiM5gzDTOomUFjJnz9dOura51mCkx0VNPpfHCiSKftU7geYQ25cAMyTsBjVxZrMt+aYH78ac5wZKKIsmYmQywJaYqszDxJvlobDIQAtLNuCfLLxQUuj/av1aepe9k/QRdZcnZlFF0XDPn5q4XHHj78fyAPCVn0tr+tbWZgZ/ZuwF9mevVst9CiDGUd6jxeWBSgfPmMDKc6mItgyK1pmQXz8P7jp08fP358H/57/PTx/YcLYKbfa18HJnwIdhYoptJSooor3MGv18mbk9o/4AcqcKYfXQsGxj+Wn374ejKih49/eXr//kMQgxj45+F9QDaD59bXP/w0efdCCp0G46Qa5L7laoLyM39xNZaWFEinncxP60y7chm9Dgz71Q8scYT96uexgz/85Zf7YFpzWkQ803D0n38av/mHn9g5mQUDdkYn0cvdbLXMVLl11jp0sedfqHZxRQlSGXYw3Y9d5jM/fU1zH/np67GNPfzl6bxJjZ96+nQa4ldf/0jv/vjXxQQ6AyZ8WLGB+zOFAub+ArCUNeqAIoBpOwQbqAxYWSe2AgyO6Oefv/55cmUf/3IVFAfp/al75Kuf8d2LgWMODG0G4HVul1tdui3Ev7pTC4GCS6eypR5cAeACu/ZIWAlmVozHj+fZMNFn/OHpwguWyiyYWEc/C6R7Jbo6nPr0SqdxC+Z0qsWUUTOKW2KuD+bh4/sLj9lPnryYDlaLcFeDEUboNNJk6WNgJXPGXluiWIK8VMetMJzTlLkBGGMJFrby9u2Tty+mtPP48Y3B+PiK7oBwNxcG0qsqtK6EC72YajZN/X/OZVaDIfeXXXRSefKCvH070Q5ZBnkVGNrYgPSXKgL/5dboOmcpgytU691sESdkZl1mNZiHV4Qx/ckL5daLty/Gr3t8XYxYCgadBj0FKU27tM6ijWIggN6PN8ulgLRr8+G1wLjquPqKP3v25BZbeeJVZuT+atXMgznSd+kiHrjSVaYKZcAKrun0ZSRKs5GlGV4n43owUFU6Nx7+Mnns7ZMnlfG9yjvbfsbab8d+s4ZqCrNgwjGIAIEqeIKEaxO62FBfA4yzPB4rIFJbBwxpAMHHaWR2opjKuxe6/fa55yVP3unP9Xf228mCjdVec28WjG/ThggAFIWjTKC1EszUWnxanLqNzOvBKIycCWpJRDNWTO05/aP/3bWr5y+ese/evn07CdAr7cwozIOpEQBTclc6ApjE9cSZggG1eEv0yWwwWwrGPFYaYtASc5pGPDDk3eyNF+/sZ+SZ/uzF22VgVNVYEgIXwPAUDC4VDzg7QdcAE0h3S6Uu7liSzkh/FRjDSsr5eAYKMC2nPHzqPvqk4m2ZeWJTLC/YZ+AzkG/G8WwMhogn+XwmripzgIx5M+OHEJuzTC9bLLaYdoLuBL1OunR3EoQ+us5M2tXnVsksgFEzQTMnJ00tY1mEve/lwufPnj2HYQOLsZ9AKHh+C5zoyXMI0O+eeCHAA2NoViMOBXbOmmtDK/fmJj5jHcL53c0O1eLqRAOcOcUUutksVNpZ/0owRMxoYGAMWFnQhAs7BvMMtPGW1d8+efH2CXnyDLWjv/s7PPjfz+bAqFaQZCzZMJR4chWYI4KNzWy9VO+mudVztd0AXX2NG/3KVUlSdP46MIZpacGgxbQtK0jnkh6ONYNp0n779taL52+fOOOv/OM5qseL1m40EzNiSM0k43LIkufALJiZMNJ3cQENxFmn3FoJJtBiaE9HKhUkidhzi0s2HmihOBWMUoYIUIKZYybprCZjxwEAXIO8ePYClPXs3TvHF+wZqunmmaClsqKcMQkxQmMwhH5FSPzjnGbCAgUz6YKvAyZNA3nrAsDM5UxfZO8PruQIRWNpWoNhLC+xj6MZJBj7GajkxT+e/X1pCwatzEiaqsgSuZELmio7BiN+53zF6dz0ejiGYKaa4CsqmiwGPUhLnNSFyLYIxheJClSiBdSFEtQsM8c0TW+I40xoP3vB6hXlxRPb/sdCp8JVjNwUFSPDmlpOU0NapplxL0Ry3/mS+aUCFIxUTDmSWLmQJguVaYHptUrVNpMKLAEzsTcae9SkGTwGnxmPcZw19cHz58///u7ti2f//eSFK1NVAISKUFNWg/CvyIKCDGJ4AYDktpaveKBg0kzZkV6KW6kZ8C/a+GynAv7rwOxTALLYtHK5TIOdGqQnhBD71tvarVv//J///ec///d//jkF5uFTwopiRpGDOUNRIEtlZCvkgllIlnNgPCmuAQb9JZFKB3BS9DowOH/EKk2RWLdzzTEC4+ksSyH3n/7iUEpyf1L7P8QmgRgX1ZMQq8RDGXAdRfN8ZhWY7uTwlzXAYC3n7FdcCYYQNtRon+QnozceP37ohC+CnbJfpsnx06f3HxoQuJyWhmhat3Ey3VAhGBoKu65mppaOXQ+m687LUrkejOuurNgAPjM1UQm6oK0/7GbO9zAfPsYGp9s7i+dCbIY1Qqp50rQscL7MTcFIK8EgCChoQPySMZ9npsB4Tm8FgZXN8oL72Ix9fH/ZVCxBnO5VCJmsyKpiUM1gNFTMVZqJCg6YwLp5xh9IFbv1er1V7bUkyZ6nM/NmhmDyZSZ/g9n9sYihIEtMnH7OaCFFHdOZK8EIfQzN2cS6YLK4pZ9KuQ10ZoGbLdFMMpk08+ZVI0ZRlj8shpS4BkFZBbKakTVRW2VmQDTP6NrqNcHUJa5YB4pdTCUSCSSawirNkIbaEJOZ5eOlomrLH49rQTNuKGYolNEgAEzyzOsr8ozDmsfhaSUYrGckKeB3A8AZObpiRfbGA9dN1EbzGBz4aixGprFcNfFM3JDjRoiwmaBhGMQLzeSbK5YJ0noG8mA6LTmHcq3YtzFfNs9XmhMwX7pzR3HrhMnnk1eDCQJ1c26JzZknxHgopOKup8xxDhdxeeolwSuWCvMDgtuReyAtWgKsqDRxnRk3WZ+x0AMYy3bBjVUmo3whZ3JXgwmdNJpO4gnNGqMYiqtQzjSCSlLDyY8x0TQPloPZrLETOpbg6KL+6wTPW8h6mwpBSfPdmbFEe26RGwyq7ZyRv8LJQZLMccNZEtjIzzwhxomZp2sYM1qc/cIYO546z/09MPauX2LwIB50Fmfj6HVShsq6zDgOlsClWfZyMJGdjAsmc3J8+6ScvLrRiVfPsTMmM1Plxxs5iOiKEodo1mRzhjUGc2dp1Ike2rvOQVwQA6q4D23VNEAxwLWYYiJbr9Ktprv28ti8ceCuvyTBTDPfSMbFq7AQ/FSKAnLjzBytGGLluCnKspKB2s6YmJmxPALEjvQzrtSmq5SgUClyKwgATTRdetZVu4cnRO3qy8PZeKWGksyxJ6qZuyL8wpAxZVGGIAbzoZln4kpQlVWFKM1MSJZDmgeGLHcafkjwKKQSZBpk9nRRzPWCiYa5KNW7RXqm2vwsgGdlwneuk8g5WTnWjJMge4Ukj9uNkzxitdrtGf2JcVZW5HhcFLHSNM2xmbHyg2XmwNcIF5Da7TqkwC5T9q/qNGFs5tJMFXf8UseZn5/xFLMfdM0/no9n8rlQ46qsaTRO2ifHJw1QZOPEnElHcUsTRdGMy0YSLwXxWDMY5LK0GY7h/EygWGba1R6utwis3OdUTgcCTM8/zjZ6ZZnTbDzwDMbUmlZTbgSvyJpK5gQ/tc0A38k3zJlEEw/GZRkqOJVkLFNWRXN8QYi2JNMIfZw5A+7YbV1UcQ3tGlscEgHuYuo4tV27v7h/ObL12nPloGbl8smMpS2PzRmGyTcamWauqcqZYGgGjBiSFU2Jy6aayVihkCyONcPGv1/c0epOz+BCS6AAgXXmNJki3WDupEx0GrIkbW4cjNeNBsshgwkpjeRSMLJmxrVMMnfSbIbM26bVmI7NYkhUTQVIAMnQBffqBIyyJJ5B/vfyn9MJX2NPQF3yu+dLcFIZAjVZdJpI9HvPymAcEHw1Vs4vW4dGrC8siL2GasbjGeZEU63pV4nOhxhqKNc0b99uHE/5nbmwPyfsw3VN48NSkWauXjzj7cOn+weqXGB3eh2Qq5h9y7vCaq5JGidfhKyTZRWN6hqfQhMMEB91OrfGc83GcaOZtOBGSJmiM4hwYU9K7Mg+8+PBVK2uSzPXWdbkHmKC9XUPgC0G54jw7XjkIVNj5DzLBOWZisYw1HiwmctZ02BkRgtNJxqRfgpeFjQzhWSmI6L5p7lLiCto0eUxgjn7lNZYO+Od44fHRGKyPSODuXgWPp2ELoitOe1YzFniTKKByy3ixnlzGkw8KCabIq4K9MAoGpTM8GRGs9gcyc2E99t7M6qJHtZsLl1m6sVsqTw53G2V0CPtUlWmlS33cF+hXenPXqRJKKMbSQ0RqJfZmAVDlpgZUh45o0Ec9sAYcVGJE9nIBLEbMDsLIP95Jori7Czdr+X29MF81lo/C7Gs2GZaKQkoQ1oC1czaWfj7KYsyGfACBoZ7Yk0HqqZTH6jmAhg0rRPnRZhnVCrNjBoKxbXZxGudTuWaiABWBmDgMtP9M+nA6vUZVFLoL4VqCZdplIoBsLPDKTvbOL09+UJiNkTQTJDEc9p0L+ZqMEho3EoAp9tCYhz4TKMhmsAFZjTDKvmpZnP0VcXGWbNUupDloKZJr7vmHMqZRK9KpYx37Om8GRGmSxfFjAeTcSaOa3yno64Hxl34vxyMGJcV04grKlQyJmvK8/MzoS+3x18rHBGg/2D7yJoTVTAzbs2tDXhOryuJdEACO5uA2Z5Zpa2aapMBM2NyqjkddT0w7pasaTBkAiYkKifEUkUozppsQ50HwybHpCZ8OTDO/OkuLoRJZ1vI7dfdF1zkvJ6mk2p1+9F4xfkfZ4hvqGnFxWDbEkPJmRlJF4wcl7GtLiricjCEhbqZKCzWMyEzN09WDca7iNFXdHeTX0rV62ma2Nfe2TC144Suip7sBdg4mP1CpQmZPwjRTD7JzZsZEXOZBu7YNOKNxjIw8WYOOB0wBKiJkvlgbkEzrOzOakZiuODcKeT96Sw9g2JNLDSeeVDSuOhMrzhTmxs7+fmWq5prGIwyCwWyIInnm3FWdKMCiTdPGqEQgsFtDR6YoJqDlwSbZiNHmmxGXigjSNCp0sJbrD51JpV3oPJ60h1vv8NNZ2mp4uyfiWz9xxI6qTaOc/MQM7TFKQenX073n0+BCeXhm3JQY4LPWMQy4V5jfqeQ8pqyGsz+s6efcevv0yq7VBsYTaHQlfySTvsae39e3rZYaJDLSTp9q83yNSWnqmJQVlwwqpbLH+O3NcxcM0m/FyrSuc+Svw/jAVuomPH5av511s1NhJ5pglCqLaaVBq+psEcxX+Tg2o7y1Aic+VoRamVjetlF/ATSfyYoHnsPqCZQTe9Lj3PW4rWitQCeC+BP1RMTODc656REz0vt1RNdPBwWrgqx+XBk31prv5jiEH2AREKQDOOTN4kYCok8PQGimpkGZoyGZS4xYaKB0wh91sbdooV6kQo9BusGYOjkZz3FJZh6IJ2FSHiGrc3wgbnGOlHibJEBSEQMhtQQ1Gfeu4wgBjOwt5k3qKaVDC434NC3UV+Yp1to8cBtz2xushmQwVMaoN7kAr1qAjeepvySjYeaCN+tsZfX5TDJkBfMoEwQXTiGRqnn/NDJFf1QowFGxneIsy4j0WKq2Wy3eOMjAap4hiXXZaqlNm4Jpm2aWHhjJ7daNXHqWRkIzO7uc5aA33u7m+KWiOlp9TWhFwQogDDy9jZziV6bnkx043OOugE87q1QYHr4+wWgGRabAZMppivFMLEAA7IVz0ychYTGPQLFbMrsNX32KTEfOLvOK2R8InJvrVWz89JLcBgyLorOHi+b7QPfjPm2v7yyD+uKivoALGpzRolyc7zU1NAaC4lp6SddhOlZOrU3uuKiqeKh6Fzxxj+/0cXf9Mi6U+g2K/DnaGi+beb6HXSQKQELIG7MGaQ8rQ2rseJTQAzcpglGZp/HBLbi5kz6SxA3P0SjnAh4B8JKZ+woFobyaIho2te6DYFQjHtkSXLhQp9MKdVortIw24hFfOFoje3wUGa6DIBLSat7/8ukPm5rOj0N5yIt42fTolhxOr2hLOnXmsnJdSDB67dskyY4fzg2ZAc4q8oPdTcIrFzLeIWMj2V0j2aDMrwCHG1j/zqLl49p8FWCy1pPcWsSg4l2XdIiFjbOhHO7Qllh+E1F9y7tbzsSqCW5WIbulDPwvRrc3DhNXolGpqu1iawtnxWAst/rzVyLhmjYaRJeVbwZFbfRfDNWNiN0IQ1gOXS7M3gKDO5zCt/NXIFGtDAuEzM45d/EUBTsWigK8DRVBPFyTvAqrgdYoP7H1D/uDdMeoJ/+Uspvk3Yae4CDyZ6z6JsaOwT+HL2bWZazieaelee6gyHHTQ3+h1MwohiP4xE0JrA10wVhzK+XncGCuzImW8TAfRDNDeqYeWkFOL32aKp/JTyq6J1NuGinuUU0iuWwFtotM74u0h4AAAljSURBVMSgpeHkuCyjTqioeJYI4Ms1km6bubk0QifHWA4nHbvoZU0J3ORQgwUpkhksoO1HNqCBC7W/sFKBeNeZGGowSXtiy9aRE7C5kJVz4CiNxRewOXpy6OaArc0c0iuMbJt7n7M0y4PLudkZ4ZFOT9PxbR3PXVXNzRxGMKfJyjIcM4jMJoa2yWyZJ0oDj87Bc+cqb2a/O9bXg++BhWF+3fbNiTBiHTTCvRn/FZ2JwVCj6W34d9bPV4bOSuba0Fl3Smxv/amazIfYeeeT/wtnAMObQ2I/mp99iHXe84TwlwvzcbFXqBsI1ttf3p5cfpmmEO1kDJAMXuGoh5vhzQ787fD9nRo+PtwZTt6lHZuznFO7hyYWhbBZmbcJXOLyfliYi7sLU1ixPvgNptHt/THFUjQZ/mtMopO98+YcwOiPaqz9Smcrj2y2hiqqdR4Npy1QzDcnYV5JHiAWwQdYXi1gibx8TyxgaPNLpRFNRR/68Mzine+cfgoxTcVMzgbaCmqGAJjaowo76A+HAwChDyud4aw7mZm415B6TVuYwmiAh40vYDm9eG8wzJ29JWggbI5i2Hk+oEflxZvxhZxBwbCd0aB/iQmjM9gaoufo82BAoxo9CjV4QI9zxrPOB4eLejn99f2xgNvMnUocjgmxy4Fz9nRke/87TVHzQXEhejlg7OFw+ApHZ7OdQwgd/eGoX5l/KR4dbL6mJhbmj2wyXPSXyN6dD4EF0cxgGQ06fOwSwk0H88CGcPBN01pCCBwwAzCzPgHkFdI/Z0ltOOj3F5fTk2bTVYsw1OFzF9YfRnzv7zCOFGaCQPiypg9jAl7BAZ5CG9nYudtccgIb+jyAeTN8NIDRDs/PebxP2PN5M8NQ+IcdPI4ywoP91s7xGs2H5Q+FBdFMB2gobMjgjRA7r7GVc4zRkfDet4unY+n0F3OIPaB/9UrNVYg9rxj59nenAvV8HnLR8DIWPhxUZreHbXw4LCDTU3KxDqvrtcuwcDnUyZDHb41E975tXMGBV/RzQrk/79FTNcM8BAq7g7/+IAxJbXrCfuPuh8TCMMIYTewVJLTh8JDnwzFwbbtPZwgiYeGgvF7Hc1rMk++3wvjREWGzo7ODR7QMxFpjOJnj/tBYGGbPRYMnDR3FYrHNGvBzgYcR1N7EonQI2/uFGxxfyJJQjtnf3qZaEWIjm/78Q5T6fjRWY8cL3T48FqbgJM8IXyFIzcDWbD4sRPlYhbDDRz46hgiEtkJOXMqWZ3EYSih570HMOVM7LGxBbtUHYLHRy8EbWqKPKt4MV+TuR/ito4tT54vtAZQAwqWub4YP+6OYsNm3CRn2fY5ZbGxvHdxrBUPL+b+DQ5WDr//4YCfq6Doau+wPWL3mQ3PlB25BxvftAfVG392P8iO1F3d9NKvFsFKqkKOYcKRXjg6jwuawQvTB0aHzIzSRjQ1h/8GD198ERbcyMwjB2llRZBln+1/febC/te2eDAz21RkQvXa0SU3Vt1nBE/sEIcx38FClD5dflqOh6hmyg1j4sqJX7MEoGuGFYQUCHP78VNjFsy3s7B+8/P7b1998842laZoFf7/59vuXB/s74PGe/8X4PrzTrkEWDsfoT6EII92+jB0NjgT8qMjey4/248EFl9kIfTyNBpta/BAoZ0SI8T78IanK4MjHe7/kAIjC4Sg9XnZ/f5+eLCtEAYeXgOFNl52BzVbowMO+gWtfHWDWtk1PIftgHGa53KFBLfpq2BfCgg5p4UgHUnjUj4ZjvnMow3QYGgTtCR2JTMkkcYQFnh91amCdtU4/hvDDWzXnJPgI1P72gDr/xulHxQIVgYPGR4v0YU237fPopm0LUYjWsdH50CZgNcM+v3nVD54hjk3haFiBV9aG55cxQeBpojyia1tj4eio0nFOU737QXjydXJBqU3YF46ylc3Lmn0O3grDOOx0DsPRmPAK9EOAIVQGnRH+OCCPIHHTJf7FnwYEjQxsXWdRJ5fg6EBca9jqAw4DBezmEXzKSKAE9uO5y5TccdiAcHTJn0NExXPVwzF6KxLDXza8fNR36n4ChGzQ6XSO+qNRH/52BrWK4RC14ejRJUIMU6rH6qAKAT4CcuXQCQQbH9ddJnLPOXEdrt8A6+cwqAiYeycWhQrskA+HIZ/jTxkOa0u4fsW1wWg4KvC+kSD4wKwqOnkj4DlZLHHa2pGNj5Ndloob1aKjYT8KeU6I9e0amJsNrBK70cBJImFqVJuXo9HoaDgYdI7gxuUONTzc7IvvRfUdRgFM7UjX+ajQrwy2HKL3e6nFkV9PKRwBvBzAvIGLOuQhDB1BYAVWgv7ju0RnD1NnwR8HjeEtGuQuX70670NgJ/ZwBN4W9tXsGrY8opB2ojTpf4hq/yZSeLnnxlqhr9tDGztDeoUXHlUGPG/bl8LRYCSMji7BnUejQ4HOS4z6wOuBfUEgM46AfdXeXLK1TezDQnENBR89RxGg/K5qceQ/T104/FHFrnRiAAoMPnbYBwJcA1Ktj6DWOhf4SgXCAOYNfgBAIarr+rADuPmaXqvgNBbcADdyqrGIb+939JZpuXPXRyNBTBgdxlBDUKkdjWKxDqYa2+b5ATmP8axdg2GD3W0S1r6M+nhb3xnBs/iyARJwflAbhX0042/sffzccpUU7pz6aNZBkoi7KIYDG6wM6kSwpBqA0RHMYGerVhlFo4dszRjyaFXAfIaxKCiQlqnRvltVApRPYGETuXDhOM5Ts/UKGBaYzegIAgFfs/sCD1nFtoHA8UP2sFIRcJ6yMuxchn18hXVWGNLfSYxs+O7++mksbArOr3e9IlQY9c9HAh7e94o/YtHFKyMAY1dsA7wbyP0A+7rAW4aUXcc6w/Gy3I2NvZefHApKASKbQ+ohgUTB5oadQ7jqh5g3DqM8O4TqHgqGTULsChnwYZ5UeMfZPT4KUO78KyBx5dfTyW/ShGPIFoc8FAoeGHYgCH22sxlDyhAbzmyVQPu696nHPy8v96bJcRTrUZ4PR4ThKDYaDIHKDYHp0J/cHf92HYT2yN6H6SF/cIHgtkcrmGlUESAJUfQRITb7ON7b+xQJcm0p3Ll7urfni0Su+bVJ58m909NPl1PWl3t3Xt49BUgQFSLzAg/BE4Dj5a+/M/96H/n1V4AEmCgqR/DO3bt3X975d8IxJYV79+79eseVX+/d+/dE8Vk+y2f5LJ/ls3yWz/JZPsv/Ifn/FtosHwoZDPMAAAAASUVORK5CYII=";

      // Insert image at top-left corner
      pdf.addImage(imageData, "JPEG", 10, 3, 25, 25);

      const startX = 10;
      const startY = 10;
      const rowHeight = 10;
      const col1Width = 70;
      const col2Width = 120;
      const tableHeight = rowHeight * 1;

      const lineHeight = 0.2; // Adjust as needed

      //MAIN TRICHY HEADING
      pdf.setFontSize(14);
      pdf.setFont("helvetica", "bold");
      pdf.text(
        "NATIONAL INSTITUTE OF TECHNOLOGY, TIRUCHIRAPALLI",
        startX + 50,
        startY - 12 + rowHeight
      );
      pdf.text("TIRUCHIRAPALLI, TAMILNADU-620015", startX + 65, startY - 5 + rowHeight);
      pdf.text("STUDENT INFORMATION FORM", startX + 75, startY + 2 + rowHeight);

      pdf.line(
        startX,
        startY + rowHeight + 8 + lineHeight,
        startX + col1Width + col2Width,
        startY + rowHeight + 8 + lineHeight
      );

      // Draw the table borders
      pdf.rect(startX, startY + 30, col1Width + col2Width, tableHeight * 3.1); // Outer rectangle
      pdf.line(
        startX + col1Width - 10,
        startY + 51,
        startX + col1Width - 10,
        startY + tableHeight * 4.1
      ); // Vertical line

      pdf.setFont("helvetica", "bold");
      pdf.text("FACULTY ADVISOR DETAILS", startX + 50, startY + 16 + rowHeight);
      // Draw the table headers
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Name:", startX + 5, startY + rowHeight * 4 - 4);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 18, startY + rowHeight * 4 - 4);

      pdf.line(
        startX,
        startY + rowHeight * 4.1 + lineHeight,
        startX + col1Width + col2Width - 40,
        startY + rowHeight * 4.1 + lineHeight
      );

      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("contact:", startX + 5, startY + rowHeight * 4.8);
      pdf.text("Department:", startX + col1Width - 5, startY + rowHeight * 4.8);

      pdf.line(
        startX + col1Width + 80,
        startY + 61,
        startX + col1Width + 80,
        startY + tableHeight * 3
      ); // Vertical line

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight * 4.8);
      pdf.text(formData.name, startX + col1Width + 55, startY + rowHeight * 4.8);

      pdf.line(
        startX,
        startY + rowHeight * 5.1 + lineHeight,
        startX + col1Width + col2Width - 40,
        startY + rowHeight * 5.1 + lineHeight
      );

      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Designation:", startX + 5, startY + rowHeight * 5.8);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight * 5.8);

      //STUDENT DETAILS

      pdf.setFontSize(14);
      pdf.setFont("helvetica", "bold");
      pdf.text("DETAILS OF STUDENT", startX + 65, startY + 67 + rowHeight);

      pdf.rect(startX, startY + 167, col1Width + col2Width, tableHeight * 9); // Outer rectangle
      pdf.line(
        startX + col1Width + 20,
        startY + 92,
        startX + col1Width + 20,
        startY + tableHeight * 2 + 112
      );

      pdf.line(
        startX + col1Width + 20,
        startY + 167,
        startX + col1Width + 20,
        startY + tableHeight * 2 + 237
      );

      //vertical line

      //ROW 1
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Name:", startX + 5, startY + rowHeight * 9);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight * 9);

      pdf.line(
        startX,
        startY + rowHeight * 9.2 + lineHeight,
        startX + col1Width + col2Width,
        startY + rowHeight * 9.2 + lineHeight
      );

      //ROW 2
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Dept:", startX + 5, startY + rowHeight * 10);
      pdf.text("Sec:", startX + col1Width + 27, startY + rowHeight * 10);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight * 10);
      pdf.text(formData.name, startX + col1Width + 55, startY + rowHeight * 10);

      pdf.line(
        startX,
        startY + rowHeight * 10.2 + lineHeight,
        startX + col1Width + col2Width,
        startY + rowHeight * 10.2 + lineHeight
      );

      //ROW 3
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Period:", startX + 5, startY + rowHeight * 11);
      pdf.text("Blood G:", startX + col1Width + 27, startY + rowHeight * 11);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight * 11);
      pdf.text(formData.name, startX + col1Width + 55, startY + rowHeight * 11);

      pdf.line(
        startX,
        startY + rowHeight * 11.2 + lineHeight,
        startX + col1Width + col2Width,
        startY + rowHeight * 11.2 + lineHeight
      );

      //ROW 4
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Cont NO:", startX + 5, startY + rowHeight * 12);
      pdf.text("DOB:", startX + col1Width + 27, startY + rowHeight * 12);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight * 12);
      pdf.text(formData.name, startX + col1Width + 55, startY + rowHeight * 12);

      pdf.line(
        startX,
        startY + rowHeight * 12.2 + lineHeight,
        startX + col1Width + col2Width,
        startY + rowHeight * 12.2 + lineHeight
      );

      //ROW 5
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Gender:", startX + 5, startY + rowHeight * 13);
      pdf.text("Email:", startX + col1Width + 27, startY + rowHeight * 13);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight * 13);
      pdf.text(formData.name, startX + col1Width + 55, startY + rowHeight * 13);

      pdf.line(
        startX,
        startY + rowHeight * 13.2 + lineHeight,
        startX + col1Width + col2Width,
        startY + rowHeight * 13.2 + lineHeight
      );

      //ROW 6
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Roll no:", startX + 5, startY + rowHeight * 14);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight * 14);



      //DETAILS OF PARENTS

      pdf.setFontSize(14);
      pdf.setFont("helvetica", "bold");
      pdf.text("DETAILS OF PARENTS", startX + 65, startY + 150 + rowHeight);

      pdf.rect(startX, startY + 82, col1Width + col2Width, tableHeight * 6); // Outer rectangle




      //ROW 1
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Father's name:", startX + 5, startY + rowHeight + 165);
      pdf.text("Mother's name:", startX + col1Width + 27, startY + rowHeight + 165);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight + 165);
      pdf.text(formData.name, startX + col1Width + 55, startY + rowHeight + 165);

      pdf.line(
        startX,
        startY + rowHeight * 10.2 + lineHeight + 77,
        startX + col1Width + col2Width,
        startY + rowHeight * 10.2 + lineHeight + 77
      );

      //ROW 2
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Occupation:", startX + 5, startY + rowHeight + 176);
      pdf.text("Occupation:", startX + col1Width + 27, startY + rowHeight + 176);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight + 176);
      pdf.text(formData.name, startX + col1Width + 55, startY + rowHeight + 176);

      pdf.line(
        startX,
        startY + rowHeight * 10.2 + lineHeight + 87,
        startX + col1Width + col2Width,
        startY + rowHeight * 10.2 + lineHeight + 87
      );

      //ROW 3
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Mobile:", startX + 5, startY + rowHeight +187);
      pdf.text("Mobile:", startX + col1Width + 27, startY + rowHeight +187);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight +187);
      pdf.text(formData.name, startX + col1Width + 55, startY + rowHeight +187);

      pdf.line(
        startX,
        startY + rowHeight * 10.2 + lineHeight +97,
        startX + col1Width + col2Width,
        startY + rowHeight * 10.2 + lineHeight +97
      );

      //ROW 4
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Whatsapp:", startX + 5, startY + rowHeight +198);
      pdf.text("Whatsapp:", startX + col1Width + 27, startY + rowHeight +198);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight +198);
      pdf.text(formData.name, startX + col1Width + 55, startY + rowHeight +198);

      pdf.line(
        startX,
        startY + rowHeight * 10.2 + lineHeight+107,
        startX + col1Width + col2Width,
        startY + rowHeight * 10.2 + lineHeight+107
      );

      //ROW 5
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("EmailID:", startX + 5, startY + rowHeight +208);
      pdf.text("EmailID:", startX + col1Width + 27, startY + rowHeight +208);

      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX + 25, startY + rowHeight +208);
      pdf.text(formData.name, startX + col1Width + 55, startY + rowHeight +208);

      pdf.line(
        startX,
        startY + rowHeight * 10.2 + lineHeight +117,
        startX + col1Width + col2Width,
        startY + rowHeight * 10.2 + lineHeight +117
      );

      //ROW 6
      pdf.setFontSize(12);
      pdf.setFont("helvetica", "bold");
      pdf.text("Permanent Address:", startX + 5, startY + rowHeight +219);
      pdf.text("Permanent Address:", startX + col1Width + 27, startY + rowHeight +219);


      // Draw the table content
      pdf.setFontSize(10);
      pdf.setFont("helvetica", "normal");
      pdf.text(formData.name, startX +10, startY + rowHeight +225);
      pdf.text(formData.name, startX + 40+col1Width , startY + rowHeight +225);

      //add a new page
      //pdf.addPage()

      // Save the PDF
      pdf.save("formData.pdf");
    }
  },
};
</script>
