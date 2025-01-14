
You can find the list of all **str** methods here: [python.org string methods](http://docs.python.org/library/stdtypes.html#string-methods).

<dl>
  <div class="row">
    <dt class="code">s.lower() / s.upper()</dt>
    <dd>Returns the lowercase or uppercase version of the string.</dd>
  </div>
  <div class="row">
    <dt class="code">s.strip()</dt>
    <dd>Returns a string with whitespace removed from the start and end.</dd>
  </div>
  <div class="row">
    <dt class="code">s.isalpha() / s.isdigit() / s.isspace()</dt>
    <dd>Tests if all the string characters are in the respective character classes: alphabetical, numeric, whitespace.
    </dd>
  </div>
  <div class="row">
    <dt class="code">s.startswith('other'), s.endswith('other')</dt>
    <dd>Tests if the string starts or ends with the given other string.</dd>
  </div>
  <div class="row">
    <dt class="code">s.find('other')</dt>
    <dd>Finds the 'other' string (not regex) within 's' and returns the first index where it begins, or -1 if it is not
      found.</dd>
  </div>
  <div class="row">
    <dt class="code">s.replace('old', 'new')</dt>
    <dd>Returns a string where all occurrences of 'old' have been replaced by 'new'.</dd>
  </div>
  <div class="row">
    <dt class="code">s.split('delim')</dt>
    <dd>
      <span>Returns a list of substrings separated by the given delimiter.</span>
      <span>For example: 
        <span class="cm-inline-code">'aaa,bbb,ccc'.split(',')</span> returns <span class="cm-inline-code">['aaa',
          'bbb',
          'ccc']</span>.
      </span>
      <span><em>Note:</em> <span class="cm-inline-code">s.split()</span> (with no arguments) splits on whitespace.</span>
    </dd>
  </div>
  <div class="row">
    <dt class="code">s.join(list)</dt>
    <dd>
      <span>Joins the elements in the given list together using the string as the delimiter.</span>
      <span>For example:
        <span class="cm-inline-code">'---'.join(['aaa', 'bbb', 'ccc'])</span> returns <span
          class="cm-inline-code">'aaa---bbb---ccc'</span>.
      </span>
    </dd>
  </div>
</dl>
